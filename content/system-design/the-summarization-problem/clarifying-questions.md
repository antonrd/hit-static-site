---
title: "Clarifying Questions"
type: docs
weight: 20
---
We already have some useful information like the expected number of requests per month and the expected latency of the responses. Given that the library could take up to 5 seconds to respond, looks like we can allow ourselves to have at most 5 more seconds of additional latency in order not to go over the 10 seconds limit. This means that it would not be feasible to have a system in which the requests are piled up and processed later. The processing must be done in real-time with no significant slow down.

However, this information is not quite enough because it would be problematic if a lot of these requests come in at the same time. Then our service would be overwhelmed to process all incoming requests and it would take a long time to respond to the ones that came last in the batch. So, it’s good to ask about this, too: what is the expected maximum number of simultaneous requests?

For this task the answer will be like that:

<blockquote>"We have some clues, which indicate that we can expect up to 50 requests per second at times. But the design should allow us to relatively easily scale up to handle more traffic in the future."</blockquote>

Another question that comes to mind is: do you want to store the results of the processing for a longer period of time? The answer is:

<blockquote>"Yes, certainly. We want to store the incoming text articles and the summary for each one of them in order to compute various statistics and also to be able to inspect the performance of our algorithms."</blockquote>

Another important question that comes to mind is related to the user experience. Waiting for 10 seconds on a web site doesn’t sound right. We should clarify what is the expected way of presenting the results within the website and the mobile app.

The interviewer will then explain:

<blockquote>"Good point! After our users send a text article through the website or the mobile app, we want to redirect them to a screen, which indicates that the summarization is in progress and update the screen with the results once they are available."</blockquote>

Here is a summary of what we know so far:

* The expected monthly requests are around 1 million
* There should be at most 50 requests per second but the architecture should easily be expandable to handle more than that, if needed
* Responses should not take more than 10 second, with the summarization library possibly taking 5 seconds to do its job
* The summaries will be presented to the users asynchronously, meaning that we will not wait for the summary to be in the HTTP response that comes after the initial HTTP request

Let’s now try to draft our high-level design.
