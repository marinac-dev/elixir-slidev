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
    <li v-click>OOP (no classes, but actors 😉 )</li>
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
      <li v-click> OTP (Erlang VM, Mnesia, Actor Model, ETS)</li>
    </ul>
    <img v-after src="assets/elixir_process.jpg" alt="Elixir process" class="w-90" v-motion :initial="{ x: -80 }" :enter="{ x: 0 }">
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

<div class="grid grid-cols-2 gap-10">
  <div>
    <h3>Primary (value types)</h3>
    <ul v-click>
      <li> Integers (arbitrary-precision) </li>
      <li> Floats </li>
      <li> Atoms  <span class="text-orange-400">true, false, nil</span></li>
      <li> Range 0..10 </li>
      <li> Regex ~r/{expression}/</li>
    </ul>
  </div>

  <div>
    <h3> Collection types </h3>
    <ul v-click>
      <li> Tuples {:ok, 42, "next"} </li>
      <li> Linked lists (closest to arrays) </li>
      <li> <div class="flex flex-row items-center"> Binaries <uim-angle-double-left /> 1,2 <uim-angle-double-right /> </div> </li>
      <li> Maps (key-value) </li>
    </ul>
  </div>

  <div class="col-span-full flex flex-col items-center">
    <h3>System types</h3>
    <ul v-click>
      <li>PID - reference to process (remote or local)</li>
      <li> Ports - reference to a port</li>
    </ul>
  </div>
</div>

---
layout: center
---

# Pattern matching and pipe operator

---

## Pattern matching

- In elixir a = 1 does not mean we are assigning 1 to a variable `a`
- Equal sign means we are `asserting` that LHS is equal to RHS. (like basic algebra)

<v-clicks>

```elixir
iex> a = 2 # Not assigning but binding
2
iex> 2 = a
2
iex> a = 1 # Rebinding
1
iex> ^a = 2 # Assert LHS to RHS without rebinding
** (MatchError) no match of right hand side value: 2
```

```elixir
iex> [1, a, 3] = [1, 2, 3]
[1, 2, 3]
iex> a
2
```

```elixir
case HTTP.get("www.totally-legit-website.com") do
  {:ok, response} -> # BUM! Do something with response
  {:error, reason} -> # Oh no :(
end
```

</v-clicks>

---

## Pipe operator

### |>

- Typical code in OOP

```elixir
people = DB.find_customers()
orders = Orders.for_customers(people)
tax    = sales_tax(orders, 2013)
filing = prepare_filing(tax)
```

<v-click>

- After rewrite

```elixir
filing = prepare_filing(sales_tax(Orders.for_customers(DB.find_customers()), 2013))
```

</v-click>

<v-click>

- But with elixir

```elixir
filing = 
  DB.find_customers()
  |> Orders.for_customers()
  |> sales_tax(2013)
  |> prepare_filing()
```

</v-click>

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
$ mix phx.new chat_app --live # LiveView flag
```

- Add authentication lib

```elixir
{:phx_gen_auth, "~> 0.7.0"}
```

- Create user auth logic

```bash
$ mix phx.gen.auth Accounts User users # Creates user with e-mail and password
```

- Create database table, CRUD logic and tests for `Room` structure.

```bash
$ mix phx.gen.live Chats Room rooms name decription user_id:references:users
```

- Create database table, CRUD logic and tests for `Message` structure.

```bash
$ mix phx.gen.context Chats Message messages content:text room_id:references:rooms user_id:references:users
```

</v-clicks>

---

## Add some style

```html
<!-- Add Font Awesome icons -->
<link rel="stylesheet" href="https://pro.fontawesome.com/releases/v5.15.3/css/all.css" />

<!-- Register icon -->
<i class="fal fa-user-edit"></i>
<!-- Login icon -->
<i class="fal fa-sign-in-alt"></i>

<!-- Chats link -->
<li>
  <%= link to: Routes.room_index_path(@conn, :index) do %>
    Chat rooms <i class="fal fa-comment-alt-lines"></i>
  <% end %>
</li>
<!-- Settings icon -->
<i class="fal fa-user-cog"></i>
<!-- Logout icon -->
<i class="fal fa-sign-out"></i>
```

---

## Lets get Room's ready

```elixir
# Add
alias ChatApp.Chats.Message
alias ChatApp.Accounts.User

# Modify
belongs_to :user, User
has_many :messages, Message
```

```elixir
# Add to Chats context
def list_room_messages(room_id) do
  query = from m in Message, where: m.room_id == ^room_id
  Repo.all(query)
end
```

---
layout: center
---

## - Elixir is Great for Everything that Runs on Top of a Socket

## - If you want to deploy and go to a vacation just choose Elixir

### not node.js 🤦‍♂️
