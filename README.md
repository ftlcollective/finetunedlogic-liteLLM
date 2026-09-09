# Fine Tuned Logic — LiteLLM

**A private, offline-capable AI setup built to run entirely on 8GB-RAM devices.**

Most AI tooling assumes fast internet, deep pockets, and cloud servers. That's not the reality for most small businesses across Africa, and it doesn't have to be. This project runs a real, usable language model directly on ordinary hardware: no subscription, no cloud dependency, and nothing typed into it ever leaves the device.

Built and maintained by [Fine Tuned Logic](https://www.linkedin.com/in/tasneemmahomed), under [FTL Collective](https://ftlcollective.github.io/ftl-portfolio/).

---

## What This Is

- A working local LLM setup, built and tested on 8GB-RAM hardware
- Built on [llama.cpp](https://github.com/ggerganov/llama.cpp), compiled from source, for full control over performance on constrained hardware
- Runs [Phi-3.1-mini-4k-instruct](https://huggingface.co/bartowski/Phi-3.1-mini-4k-instruct-GGUF) (Q4_K_M quantization, ~2.4GB) as the default model
- Accessible from any device on the same network, laptop or mobile, not just the machine running it
- Designed for the hardware realities of African SMEs: low RAM, unreliable connectivity, and data that needs to stay private
- Paired with a full step-by-step guide (included in this repo as a PDF) so anyone can set this up themselves, technical or not

## Requirements

- A machine with **8GB RAM** (no GPU required)
- **Windows:** [w64devkit](https://github.com/skeeto/w64devkit/releases) (build toolchain) and [CMake](https://cmake.org/download) (added to PATH during install)
- **Mac/Linux:** a standard C++ build toolchain (Xcode Command Line Tools / build-essential) and CMake
- ~3GB free disk space for the model

## Setup

```bash
# 1. Clone this repo (or llama.cpp directly)
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp

# 2. Build it
cmake -B build
cmake --build build --config Release

# 3. Download a model
# Get Phi-3.1-mini-4k-instruct-Q4_K_M.gguf from:
# https://huggingface.co/bartowski/Phi-3.1-mini-4k-instruct-GGUF
# and place it in the models/ folder

# 4. Run it
build/bin/llama-cli -m models/Phi-3.1-mini-4k-instruct-Q4_K_M.gguf -p "Hello, introduce yourself"
```

That's it, fully offline from here.

## Using It From Your Phone

The setup above runs on one machine. To make it reachable from a phone or any other device on the same WiFi:

```bash
build/bin/llama-server -m models/Phi-3.1-mini-4k-instruct-Q4_K_M.gguf --host 0.0.0.0 --port 8080
```

Then, on your laptop, find its local network IP address (`ipconfig` on Windows, `ifconfig` on Mac/Linux, look for the IPv4 address on your active WiFi adapter). On your phone, connect to the **same WiFi network** and open `http://<that-ip>:8080` in a browser.

Note: this only works while both devices share the same local network and the laptop stays on and running. It is not internet-wide access, which is intentional, nothing leaves the local network.

## Full Guide

The complete walkthrough, written for a mixed technical and non-technical audience, is included in this repo:

**[Running_Your_Own_LLM_on_8GB_RAM.pdf](./Running_Your_Own_LLM_on_8GB_RAM.pdf)**

It covers picking the right model size and quantization level, the difference between llama.cpp and Ollama, wiring it into an actual chat interface, and managing performance on constrained hardware.

## Why This Matters

Cloud AI tools quietly assume infrastructure most SMEs in this market don't have, and route sensitive business data through servers outside the country in the process. This project is a working example that a real, private AI setup doesn't need either of those things. It's part of ongoing work under Fine Tuned Logic to bring practical automation, app, web, and AI/LLM solutions to businesses across South Africa.

## Get in Touch

Interested in a similar setup for your own business, or want to learn how to build this yourself?

- Email: tasneem@ftlcollective.org
- LinkedIn: [linkedin.com/in/tasneemmahomed](https://www.linkedin.com/in/tasneemmahomed)

---

*Fine Tuned Logic, built for the hardware realities of the African market.*
