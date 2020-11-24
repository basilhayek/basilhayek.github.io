---
title: "Creating a Reading Queue in Notion: Part 1"
---
I have a problem with books. I might say that I buy too many. Perhaps this is true, but the reality is I finish too few.

I always find books that pique my interest (thanks Amazon recommendations!) and end up either buying them (thanks Amazon digital credits!) or if I'm being a bit more disciplined, I just download a sample. But this leads to an ever growing queue on my Kindle app.

I'd love to have a set of "slots" to manage the different kinds of book I'm reading. For me, this would probably mean a slot each for fiction and short stories, and then a few slots for different kinds of non-fiction. Perhaps a slot for non-fiction books that I want to be able to think deeply about, a slot for quick hits, and a slot for something in the middle. 
<!--excerpt-->

The collection feature on Amazon's Kindle devices and app are lackluster at best. App collections don't sync with devices, and they don't support the concept of queues. They also require a few steps to add a book to a collection (e.g., send the book to Kindle, click the hamburger / overflow menu, click Add to Collection, choose the collection, then click OK). Five steps. I want to add books to my queue more quickly.

I've seen different reading dashboards on Notion, and so I'm thinking that I'll manage my book queue there.

## The idea

I built a little SMS app that I call "MyScribe" that is a rudimentary list building app. I use it for quick notes, and to catalog my son's ever-expanding collection of Lego.

My plan is to be able to:
1. Send an SMS to MyScribe containing an Amazon URL, Good Reads URL, or book title and category tag
2. Have the book information (cover art, title, author) pulled and added to a Notion list

### Components

I'll need three components for this. I'll start with Notion and work backwards from there.
- [ ] **MyScribe**: need to update it to correctly interpret a book URL
- [ ] **Good Reads**: need to be able to extract book information
- [ ] **Notion**: create a new entry with the cover art, title, and author in the appropriate list

## Notion

Notion does not have a formal API, but there are unofficial APIs that are the result of [reverse engineering the underlying Notion calls](https://medium.com/@jamiealexandre/introducing-notion-py-an-unofficial-python-api-wrapper-for-notion-so-603700f92369) and creating a library around that. I'll be using Jamie Alexandre's [notion-py](https://github.com/jamalex/notion-py).

### Getting set up

For the initial exploration, I'm going to use [repl.it](https://repl.it/@basilhayek/Notion-Sample#main.py) to play around with the API. Access to Notion requires a token embedded in a cookie. Since I want to keep this safe, I'll be using a [.env file on repl.it](https://docs.repl.it/repls/secret-keys) to store it. A quick test using an incognito window shows that anything I put into the .env file will not be visible to anyone else viewing the public repl.
![Able to view token as repl owner](https://cdn.basilhayek.com/02-notion-book-queue/01-repl-it-owned-access-test.png)
*Able to view token as repl owner*

![Not able to view the token as a guest](https://cdn.basilhayek.com/02-notion-book-queue/02-repl-it-guest-access-test.png)
*Not able to view the token as a guest (phew)*

So next to run the example from Jamie Alexandre's repo and make sure everything works:

```python
import os
from notion.client import NotionClient

# Obtain the token_v2 value by inspecting your browser cookies on a logged-in (non-guest) session on Notion.so
secret_token = os.getenv("TOKEN")

if secret_token:
  client = NotionClient(token_v2=secret_token)

  test_page = os.getenv("TEST_PAGE")

  # Replace this URL with the URL of the page you want to edit
  page = client.get_block(test_page)

  print("The old title is:", page.title)

  # Note: You can use Markdown! We convert on-the-fly to Notion's internal formatted text data structure.
  page.title = "The title has now changed, and has *live-updated* in the browser!"
else:
  print("Fork this and create your own .env file with your TOKEN and TEST_PAGE")
```

After a quick test run, it looks like I'm ready to go--but that's for next time.

![Running my script and seeing it pull the current page title](https://cdn.basilhayek.com/02-notion-book-queue/03-repl-it-updated-page.png)
*Running my script and seeing it pull the current page title*

![Seeing the updated page name in Notion](https://cdn.basilhayek.com/02-notion-book-queue/04-notion-page-updated-title.png)
*Seeing the updated page name in Notion*