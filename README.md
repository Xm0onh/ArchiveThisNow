# ArchiveThisNow!

A Twitter bot that automatically archives tweets and their media to Autonomys Network decentralized storage using AutoDrive.

## Overview

ArchiveThisNow! listens for Twitter mentions and DMs containing tweet links, then permanently stores those tweets (including text, photos, and videos) on the Autonomys Network using the AutoDrive API. Once archived, users receive a reply with the Content ID (CID) and a link to access the archived content.

## Features

- Archives tweets mentioned in replies via Twitter mentions
- Archives tweets shared via Twitter DMs
- Stores tweet text, photos, videos, and thread context
- Generates AI-powered commentary about archived tweets using LangChain
- Provides CID and access link to users with intelligent context

## Prerequisites

- Node.js (v20+)
- Yarn Berry
- Twitter account credentials
- [AutoDrive API key](https://ai3.storage/)
- OpenAI API key or Anthropic API key (for LLM commentary)

## Installation

1. Clone the repository
2. Install dependencies:
   
   ```
   yarn install
   ```
4. Copy `.env.sample` to `.env` and fill in the required credentials:
   
   ```
   cp .env.sample .env
   ```

## Configuration

Edit the `.env` file with your credentials:

```
# Twitter credentials
TWITTER_USERNAME=your_twitter_username
TWITTER_PASSWORD=your_twitter_password

# AutoDrive API key
AUTO_DRIVE_API_KEY=your_auto_drive_api_key

# Optional: Password for encrypting stored tweets
AUTO_DRIVE_PASSWORD=optional_password_for_encryption

# LLM Configuration
LLM_PROVIDER=openai  # Choose 'openai' or 'anthropic'

# For OpenAI
OPENAI_API_KEY=your_openai_api_key
OPENAI_MODEL=gpt-4  # Optional, defaults to gpt-4

# For Anthropic (alternative to OpenAI)
ANTHROPIC_API_KEY=your_anthropic_api_key
ANTHROPIC_MODEL=claude-3-sonnet-20240229  # Optional

# Spawn intervals (in milliseconds)
DMS_SPAWN_INTERVAL=900000  # 15 minutes
MENTIONS_SPAWN_INTERVAL=900000  # 15 minutes
```

## Usage

### Test LLM Configuration

Before running the bot, you can test your LLM configuration:

```
yarn test-llm
```

This will verify that your API keys are working and that the LLM can generate commentary.

### Run

```
yarn start
```

## How It Works

1. The bot authenticates with Twitter using provided credentials
2. It monitors for:
   - Twitter mentions containing tweet URLs
   - DMs containing tweet URLs
3. When a tweet URL is detected, it:
   - Fetches the tweet data
   - Downloads any media (photos, videos)
   - Uploads everything to AutoDrive
   - Generates AI-powered commentary about the tweet content using LangChain
   - Replies to the user with intelligent commentary, CID, and access link
