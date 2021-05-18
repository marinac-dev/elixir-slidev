---
layout: cover
highlighter: shiki
background: "./assets/elixir-bg.png"
info: |
  ## Presentation created by Nikola Đorđević
  ### 2021. BadinSoft.
---

<h1 class="pl-16 font-sans text-purple-600"> Elixir </h1>

<div class="bg-opacity-40 bg-dark-600 w-86 p-2 rounded text-center">
Programming language of the future
</div>

---

# What is Elixir?

<div class="flex flex-row w-full">
  <ul class="w-1/2">
    <li v-click>Functional</li>
    <li v-click>OOP (no classes 😉 )</li>
    <li v-click>Dynamic (strong)</li>
    <li v-click>Concurent</li>
    <li v-click>General purpose</li>
    <li v-click>Immutable</li>
    <li v-click>Distributed</li>
    <li v-click>Fault-tolerant</li>
    <li v-click>Productive</li>
    <li v-click>Awesome! 🤍</li>
  </ul>

  <div class="w-1/2">
    <h2 v-click>Who uses Elixir/Erlang?</h2>
    <ul v-click>
      <li>
        Discord uses Elixir for their large-scale messaging system. Using Rust to Scale Elixir from 5 to 11 Million Concurrent Users 😮
      </li>
      <li>
        WhatsApp - 2 Million connections on one node/server, Facebook (chat backend)
      </li>
      <li>
        Motorola Solutions uses Erlang and Elixir for mission-critical communication systems that need to be reliable and fault-tolerant.
      </li>
      <li>
        Moz uses Elixir for the backend of their digital marketing and SEO toolset, Moz Pro
      </li>
    </ul>
    <div v-click>
      <h3>A happy accident?</h3>
      <p class="text-sm">Created by Jose Valim ~ 2011, accidentally 😆</p>
    </div>
  </div>
</div>

---
background: "./assets/gradient.svg"
---

# Pros/Cons

<div class="flex flex-row items-stretch justify-around">
  <div>
    <h2>Pros</h2>
    <ul>
      <li v-click> Concurrency </li>
      <li v-click> Scalability </li>
      <li v-click> Fault tolerance </li>
      <li v-click> Phoenix framework </li>
      <li v-click> OTP </li>
      <li v-click> Erlang VM </li>
    </ul>
  </div>

  <div>
    <h2> Cons </h2>
    <ul>
      <li v-click> Immature ecosystem </li>
      <li v-click> Weak FLOPS game </li>
      <li v-click> Small community </li>
      <li v-click> Small tallent pool </li>
    </ul>
  </div>
</div>

---

# Elixir vs Everybody

<div class="flex pt-20">
  <img src="assets/erlang_vs_everybody.png" class="w-3/4 m-auto" alt="Elixir versus everybody">
</div>
---

# Benchmark

<div class="flex pt-10">
  <img src="assets/phoenix_performance.png" class="w-3/4 m-auto" alt="Elixir versus everybody">
</div>

---
layout: center
background: "./assets/elixir-2bg.png"
---

# Data types in Elixir

---

<div class="grid grid-cols-2 gap-10">
  <div>
    <h2>Primary (value types)</h2>
    <ul v-click>
      <li> Integers (arbitrary-precision) </li>
      <li> Floats </li>
      <li> Atoms  <span class="text-orange-400">true, false, nil</span></li>
      <li> Range 0..10 </li>
      <li> Regex ~r/{expression}/</li>
    </ul>
  </div>

  <div>
    <h2> Collection types </h2>
    <ul v-click>
      <li> Tuples {:ok, 42, "next"} </li>
      <li> Linked lists (closest to arrays) </li>
      <li class="flex flex-row items-center">
        Binaries <uim-angle-double-left /> 1,2 <uim-angle-double-right />
      </li>
      <li> Maps (key-value) </li>
    </ul>
  </div>

  <div class="col-span-full flex flex-col items-center">
    <h2>System types</h2>
    <ul v-click>
      <li>PID - reference to process (remote or local)</li>
      <li> Ports - reference to a port</li>
    </ul>
  </div>
</div>

---
layout: center
---

# Developing in Elixir

### Quick prototyping

---

## Simple chat app

<v-clicks>

- Create simple Elixir project

```bash
$ mix phx.new chat_app
```

- Add authentication lib

```elixir
{:phx_gen_auth, "~> 0.7.0"}
```

- Create user auth logic

```bash
$ mix phx.gen.auth Accounts User users username
```

- Create database table, CRUD logic and tests for `Message` structure.

```bash
$ mix phx.gen.html Accounts Message messages content:text user:references:users
```

- Create database table, CRUD logic and tests for `Room` structure.

```bash
$ mix phx.gen.html Accounts Room rooms name decription
```
</v-clicks>

---
layout: center
---

## If you want to deploy and go to a vacation just choose Elixir

### not node.js 🤦‍♂️
