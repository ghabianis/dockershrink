# DockerShrink

**Dockershrink is an AI-powered Commandline Tool that helps you reduce the size of your Docker images.**


![Typical interaction with dockershrink CLI](./assets/images/dockershrink-how-it-works.gif)


It combines the power of traditional Rule-based analysis with Generative AI to apply state-of-the-art optimizations to your Image configurations :brain:

Dockershrink can automatically apply techniques like Multi-Stage builds, switching to Lighter base images like alpine and running dependency checks. PLUS a lot more is on the roadmap :rocket:

Currently, the tool only supports [NodeJS](https://nodejs.org/en) applications.


> [!IMPORTANT]
> Dockershrink is **BETA** software.
> 
> We would love to hear what you think! You can provide your feedback by [creating an Issue](https://github.com/duaraghav8/dockershrink/issues) in this repository.


## Why does dockershrink exist?
Every org using containers in development or production environments understands the pain of managing hundreds or even thousands of bloated Docker images in their infrastructure.

But not everyone realizes that by just implementing some basic techniques, they can reduce the size of a 1GB Docker image down to **as little as 100 MB**!

([I also made a video on how to do this.](https://youtu.be/vHBHxQfK6cM))

Imagine the costs saved in storage & data transfer, decrease in build times AND the productivity gains for developers :exploding_head:

Dockershrink aims to auomatically apply advanced optimization techniques so engineers don't have to waste time on it and the organization still reaps the benefits!

You're welcome :wink:



## How it works
Currently, the CLI is the primary way to interact with dockershrink.

When you invoke it on your project, it analyzes code files.

Dockershrink looks for the following files:

:point_right: `Dockerfile` (Required)

:point_right: `package.json` (Optional)

:point_right: `.dockerignore` (Optional, created if doesn't already exist)

It then creates a new directory (default: `dockershrink.optimized`) inside the project, which contains modified versions of your files that will result in a smaller Docker Image.

The CLI outputs a list of actions it took over your files.

It may also include suggestions on further improvements you could make.


## Installation
**TODO**


## Usage

Navigate into the root directory of one of your Node.js projects and invoke dockershrink with the `optimize` command:

```bash
$ dockershrink optimize
```

Dockershrink will create a new directory with the optimized files and output the actions taken and (maybe) some more suggestions.

For detailed information about the `optimize` command, run

```bash
dockershrink optimize --help
```


### Using AI Features

> [!NOTE]
> Using AI features is optional, but **highly recommended** for more customized and powerful optimizations.
>
> To use AI, you need to supply your own OpenAI API key, so even though Dockershrink itself is free, openai usage might incur some cost for you.

By default, dockershrink only runs rule-based analysis to optimize your image definition.

If you want to enable AI, you must supply your [OpenAI API Key](https://openai.com/index/openai-api/).

```bash
dockershrink optimize --openai-api-key <your openai api key>

# Alternatively, you can supply the key as an environment variable
export OPENAI_API_KEY=<your openai api key>
dockershrink optimize
```

> [!NOTE]
> Dockershrink does not store your OpenAI API Key.
>
> So you must provide your key every time you want "optimize" to use AI features.


### Default file paths
By default, the CLI looks for the files to optimize in the current directory.

You can also specify the paths to all files using options (see `dockershrink optimize --help` for the available options).


## Development

> [!NOTE]
> If you're simply interested in using Dockershrink, you can skip this section.

1. Clone this repository
2. Navigate inside the root directory of the project and create a new virtual environment
```bash
python3 -m venv .venv
source .venv/bin/activate
```
3. Install all dependencies
```bash
pip install --no-cache-dir -r requirements.txt
```
4. Install the editable CLI tool
```bash
# -e ensures that the tool is editable, ie, code changes reflect in the tool immediately, without having to re-install it
pip install -e .

# Try running the cli
dockershrink --help
```
5. Make your code changes
6. Run black
```bash
black .
```
7. In case of any changes in dependencies, update requirements.txt
```bash
pip freeze > requirements.txt
```
