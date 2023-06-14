---
title: "Wordle Game Telegram Bot in Go"
date: 2023-06-14T15:20:39+03:00
tags: ['go', 'golang', 'game', 'telegram', 'bot']
categories: ['Coding']
---

# Introduction
Being mainly a Java programmer, I decided however to expand my area of knowledge and the fates fell on the Go language. 
And the best way to learn is to apply, to practice what you learn!
I usually prefer to do this by implementing a game or a tool that has some use. 
So this time it's a game - [Wordle](https://en.wikipedia.org/wiki/Wordle) but implemented as a [Telegram Bot](https://core.telegram.org/bots).

# Environment
To run Go code, you need to install Go on your local computer. In my case, I'm using Windows 10, so I installed the latest version of Go, which is currently 1.20.5, from their [website](https://go.dev/dl/). For development, I use Visual Studio Code as my IDE.

## Telegram Bot
![tbotfather.jpg](https://i.postimg.cc/V6fk4Rgj/tbotfather.jpg)  
I created my Telegram Bot using [The Botfather](https://t.me/botfather). 
For more information check the official documentation available [here](https://core.telegram.org/bots/tutorial). 
To create a bot, you need to communicate to [The Botfather](https://t.me/botfather) and request a new bot with the command  
```
/newbot
```

# Wordle Game
The Wordle Game involves guessing a five-letter word chosen by the computer. You have six attempts to guess the word, with feedback given for each guess in the form of colored tiles indicating when letters match or occupy the correct position. These tiles indicate whether the letters match or occupy the correct position. However, due to the nature of Telegram, we can only provide feedback to the user using text characters, such as letters and symbols:
 - Bold letter - indicates the letter is in the correct position.
 - Italic letter - indicates the letter is present but not in the correct position.
 - \# - indicates the letter is not present in the word.

 # Implementation
 You can find the game implementation in this GitHub repository [https://github.com/prutonis/wordlebot](https://github.com/prutonis/wordlebot).
 Some key points to mention are that I used [yanzay](https://github.com/yanzay/tbot/)'s Bot library to communicate with Telegram Bot API. Also I used [zap](https://pkg.go.dev/go.uber.org/zap) library for logging, the [viper](https://github.com/spf13/viper) for storing and reading configuration files, and [GoDtoEnv](https://github.com/joho/godotenv) library for reading **.env** file where the Bot Token is stored.  
 
 
If you have access to a Docker instance, you can run the bot within seconds by following these instructions:
 1. Clone the repository
 ```git
$ git clone https://github.com/prutonis/wordlebot
 ```
 2. Navigate to the **wordlebot** directory and set your Bot token in the `.env` file:
 ```
 $ cd wordlebot
 $ echo TBOT_TOKEN=4839574812:AAFD39kkdpWt3ywyRZergyOLMaJhac60qc > .env
 ```
 3. Build the Docker image
 ```
 $ docker build -t wordlebot .
 ```
 4. Start a Docker container from the created image:
 ```
 $ docker run --name wordle_game --rm -d -t wordlebot
 ```
 Now, you can enjoy the game. Simply open your bot in Telegram and type `/start` or `/help` to begin.


# Features
The help menu of the game:  
![help.png](https://i.postimg.cc/jdkN5c03/help.png)

You can choose between English and Romanian languages:
![pick-language.png](https://i.postimg.cc/t4ChXzR7/pick-language.png)

An example of gameplay:
![gamplay.png](https://i.postimg.cc/fWYPpx0q/gameplay.png)