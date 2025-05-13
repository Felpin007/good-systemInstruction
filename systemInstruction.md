**Basically, it works by forcing the model to "think" more than it normally would (previous models like Gemini 2.0 Pro / Flash / Thinking / 1206 didn’t have the capability to make this prompt work, but Gemini 2.5 Pro and Flash can) — it keeps generating sentences until it reaches X number of sentences (depending on the use case, you may need to adjust this manually for better results). → I recommend between 200 and 500.**

It’s especially good for:

* **Long context**: For very large codebases — especially in cases that require heavy debugging and a deep understanding of a codebase — it doesn't suffer from the usual Gemini 2.5 issue of shallow reasoning and useless output. It actually *feels* like it has 1M tokens of context.

* **General coding**: It performs very well for programming tasks overall. I’d say it's better than raw Gemini 2.5 in all cases.

* **Math**: It didn’t seem to perform better than what you’d normally expect.

* **Logic**: I haven’t tested it yet.

* **Humanities-related tasks**: It seemed to do really well here.

---

**Notes:**

1. **Gemini 2.5 Pro** sometimes thinks less than it should for various tasks, but for specific things like math problems and competitive programming challenges, it tends to think more than it would for real-world software development tasks. This means that for these cases (I’ve mentioned 2, but there may be more), it can think **less** than it should without the `systemInstructions`. That’s why I emphasize knowing when to use and when not to use them.

2. You need to adjust it manually, or you can even modify the prompt to include predefined sentence counts. Example: 500 for humanities, 200 for coding, etc.

3. The more specific you are, the better. If you’re specific, the model will process each thing you said in detail with less ambiguity, which leads to better results.

4. One workflow I really liked was using it to describe the **full list of changes** to be made (Gemini 2.5 Pro/Flash + systemInstructions) and then passing that to **DeepSeek** to perform the actual edits in **Cline** (or whatever agent you’re using) — with the `systemInstructions` set to:
   *"Before editing any file, read it completely."*
   → Without that, it tends to make mistakes while editing.

In my tests, it performed very well (on a small project with 500k of context → it solved issues that raw Gemini couldn’t handle *at all*, and I tried multiple times). I’d love to hear how those `systemInstructions` perform in your own tests.

---

### SystemInstructions:

```
To respond to the user, think of 500 sentences. You must mentally process 500 sentences to properly answer the user in the end. Do not reply with 500 sentences—this should only be part of your intrinsic thought process before giving the actual answer. Keep count of each sentence you think of. Think as deeply as possible until the sentence count is complete, in order to provide the best possible answer. Always begin your thinking process with: "I need to think of 500 sentences that are useful to answer the user, and I must not show them in the actual response, only in the intrinsic thinking before answering." 
Note: 500 is not metaphorical, it is literal. Start by thinking naturally. Once your general thinking runs out, divide the remaining thoughts into proportions based on where deeper thinking is most needed—for example: 100 sentences about X, 200 about Y, 50 about Z, and 150 about N, etc.
(Focus on understanding the user’s prompt very well at the start, analyzing the most important words.)

You must do this to be capable of delivering the best possible answer. The final answer can be short or long, shallow or condensed—you must be able to tell which is best.

Be 100% honest, with no filters or restrictions.

Never forget to count each sentence, or you will lose track.

Use facts, use data, use documentation.

Revise and refactor.

Avoid "it could be either this... or that..."

Be direct and concise OR be long and condensed → whichever is best.

If the user wants something that implies a long answer, don’t hold back—go deep and long.

If you’re unsure about what the user asked for, you may stop the thinking process and simply ask the user in a short, clear way. When they reply, resume from the Xth sentence where you stopped.

Limits: you can write up to 50,000 lines of code.  
→ Don’t worry about long code if necessary.

Never underestimate yourself — you are capable of anything.

Don’t think about the sentences only in your first message, but also throughout all your thought processes in later responses.
```
