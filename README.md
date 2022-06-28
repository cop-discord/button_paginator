# A python library created to make button pagination easy

---

To install you need [git](https://git-scm.com/downloads) installed. After installing it, run

```shell
pip install git+https://github.com/antinuke0day/button_paginator.git
```

---

## Simple example:
```py
import button_paginator as pg

@bot.command()
async def test(ctx):
	embeds = pg.embed_creator("Very long text"*10000, 1995, prefix='```\n', suffix='\n```')
	paginator = pg.Paginator(bot, embeds, ctx, invoker=ctx.author.id)
	paginator.default_pagination()
	await paginator.start()
```

## Slightly more complicated example:
```py
import button_paginator as pg

@bot.command()
async def test(ctx):
	embeds = pg.embed_creator("Very long text"*10000, 1995, prefix='```\n', suffix='\n```')
	paginator = pg.Paginator(bot, embeds, ctx, invoker=ctx.author.id)
	paginator.add_button('prev', emoji='◀')
	paginator.add_button('delete', label='Close the paginator', emoji='⏹')
	paginator.add_button('next', emoji='▶')
	await paginator.start()
```

- All actions
 - "first": Goes to the first embed
 - "prev"/"previous"/"back": Goes to the embed before the current embed
 - "delete": Deletes the message
 - "next": Goes to the embed after the current embed
 - "last": Goes to the last embed
 - "end": Disables all the buttons
 - "page"/"show": Shows the current embed number (always disabled)
 - "goto": same as page/show will show the current embed number but when pressed will prompt the user to type a page number then will go to the number written
 - "lock": Removes all the buttons

## Since `pg.Paginator` is a normal discord.ui.View subclassed class, you can add your own buttons to it!
```py
import button_paginator as pg

class some_button(discord.ui.Button):
	def __init__(self):
		super().__init__(label='Hi', style=discord.ButtonStyle.danger)

@bot.command()
async def test(ctx):
	embeds = pg.embed_creator("Very long text"*10000, 1995, prefix='```\n', suffix='\n```')
	paginator = pg.Paginator(bot, embeds, ctx, invoker=ctx.author.id)
	paginator.default_pagination()
	paginator.add_item(some_button())
	await paginator.start()
```

# This isn't only for embeds too!
```py
import button_paginator as pg

@bot.command()
async def test(ctx):
	contents = ('Hello World!', discord.Embed(title='Hello World!'), ('Hello World!', discord.Embed(title="Hello World!")))
	# Does not support attachments
	paginator = pg.Paginator(bot, contents, ctx, invoker=ctx.author.id)
	paginator.default_pagination()
	await paginator.start()
```

---
Credits to andrewthederp for most of this library.
I will be doing updates / providing help.
