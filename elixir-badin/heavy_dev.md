---

## Simple chat app

<v-clicks>

- Install Elixir & Phoenix from official website

```html
elixir-lang.org/install.html
hexdocs.pm/phoenix/installation.html
```

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
# File `/lib/chat_app/chats/room.ex`
# Add
alias ChatApp.Chats.Message
alias ChatApp.Accounts.User
# Modify
belongs_to :user, User
has_many :messages, Message

# Update changeset
|> cast(attrs, [:name, :decription, Add -> :user_id])
```

<v-click>

## And messages

```elixir
# File `/lib/chat_app/chats/message.ex`
# Add
alias ChatApp.Chats.Room
alias ChatApp.Accounts.User
# Modify
belongs_to :users, User
belongs_to :rooms, Room

# Update changeset
|> cast(attrs, [:name, :decription, Add -> :user_id])
```

</v-click>

---

## Update user and contexts

- Add rooms and messages to the user

```elixir
# File `/lib/chat_app/accounts/user.ex`
# Add
alias ChatApp.Chats.{Room, Message}

has_many :rooms, Room
has_many :messages, Message
```

- Lets add fn to list last 50 messages for given `room_id`

```elixir
# File `/lib/chat_app/chats.ex`
# Add new messages fn to Chats context
def list_room_messages(room_id) do
  query = from m in Message, where: m.room_id == ^room_id, limit: 50
  Repo.all(query)
end
```

---

## Sending messages??
