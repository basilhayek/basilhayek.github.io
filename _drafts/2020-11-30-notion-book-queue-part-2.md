---
published: false
---
# Creating a Reading Queue in Notion
## Part 2: Full integration with Notion

In my [last post](https://www.basilhayek.com/2020/11/24/notion-book-queue-part-1.html), I set out to create a way to manage my ever-expanding list of books to read. After creating the "Hello World" equivalent of connecting to Notion (thanks to this excellent unofficial API), it was time to get to work actually managing a queue in Notion.

The three components listed below are the same as before, but just listed in the order I'm working on them. Success for this step is being able to create a new entry in my book queue.

1. Notion: create a new entry with the cover art, title, and author in the appropriate list
2. Good Reads: need to be able to extract book information
3. MyScribe: need to update it to correctly interpret a book URL

That first piece has a few steps within it: 
1. I'll need to create the appropriate data structure in Notion. I'm thinking of the gallery view, since it's always nice to see the cover of a book
2. I'll then need to work with the API to actually create a new entry in that queue

### Setting up the book queue data structure in Notion
I created three queues to allow me to test the code I was developing:
* Short-Non Fiction
* Non Fiction
* Short Stories

For each queue, I set up a gallery with the following attributes:
* Name: title of the book
* Created: when the book was added; uses a Notion formula to populate
* Category: added this before I decided to use separate databases; I'll just keep it for now
* Status: one of Queued, Reading, Read, Abandoned
* Started: data I moved this book to "Reading" status
* Finished: data I moved this book to "Read" status
* Reference_URL: e.g., to an Amazon or Goodreads page
* isbn: added this later, as I realized it would help with retrieving book information, such as the cover art--more on that later

### Using the API to create an entry
This part was a bit tricky. It took reading the examples, the source code, and a healthy dose of trial-and-error to wrap my head around the ```CollectionViewBlock``` and ```CollectionView``` and ```Collection``` objects. It probably took me longer to get there because I needed to use ```client.get_block()``` method as opposed to the ```client.get_collection_view()``` in the code sample. This was because I wanted to have a single page with multiple queues, and want to be able to target any one of those queues in a single method call.

The code below was the first cut of successfully creating a new book within one of the queues. I rather lazily iterate through each ```CollectionViewBlock``` on the page and add a new entry to the last one. I also iterate through each view, although from the perspective of adding a book, I could probably just choose the first one. 

```python
import os
from notion.client import NotionClient
from notion.block import CollectionViewBlock

# Obtain the `token_v2` value by inspecting your browser cookies on a logged-in (non-guest) session on Notion.so
secret_token = os.getenv("TOKEN")

def view_cvb(client, cvb):
  for view in cvb.views:
    for row in view.default_query().execute():
      print("{}".format(row.name))
  row = view.collection.add_row()
  row.name = "A new book"

if secret_token:
  client = NotionClient(token_v2=secret_token)

  test_page = os.getenv("TEST_PAGE")

  # Replace this URL with the URL of the page you want to edit
  page = client.get_block(test_page)
  print("Page title is:", page.title)

  for child in page.children:
    print("{} is {}".format(child.title, type(child)))
    if(isinstance(child, CollectionViewBlock)):
      view_cvb(client, child)

else:
  print("Fork this and create your own .env file with your TOKEN and TEST_PAGE")
```

Finished queues
