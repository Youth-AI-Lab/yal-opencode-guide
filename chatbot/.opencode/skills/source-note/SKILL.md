---
name: source-note
description: Writes a new document for the knowledge/ folder from information given by the user. Use when the user wants to add, correct or document something the chatbot should know, or says "add this to the knowledge", "note this source", "that's wrong, the right answer is…".
---

# Writing a document for knowledge/

You turn what the user tells you into a short document in the `knowledge/` folder, so that the
chatbot can use it in later conversations.

## Steps

1. Ask for the **source** if it is not given: who says it, the title of the document or page,
   its address and its date. Without a source, you still write the document, but you put
   `Source: TO BE COMPLETED` on the second line and you tell the user.
2. Rephrase in short sentences, one fact per sentence. Add no fact the user did not give.
   Do not complete it with your own knowledge.
3. Choose a file name: `NN-short-topic.md`, NN a number between 10 and 89 that no other
   document of `knowledge/` uses.
4. Write the file with this layout:

   ```
   # <title>
   Source: <who, title, address, date>
   Written from what <the user> said on <today's date>. Not yet checked by another person.

   <the facts, one per sentence>
   ```

5. Add one line for it at the end of `knowledge/index.md`, in the same form as the others.
6. Show the document to the user and ask them to check it.
7. If the document contradicts another document of `knowledge/`, say so explicitly and offer to
   update or delete the old one. Do not decide alone.

## What you don't do

- Invent a source, an organisation or a figure to "complete" the document.
- Change an existing document without the user's agreement.
- Create or change a file with a shell command (`cat >`, `sed -i`, `echo >`…): use the write and
  edit tools, so that the person sees exactly what changes before accepting.
