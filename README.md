#AI  exploration and summary based on programming, drawing, and writing (18 bans) —— February 2023 edition
 
Catalog introduction
 
Stable Diffusion Simple Tutorial: [ Stable Diffusion ](./stable-diffusion)
 
Jupyter related parts
 
- [ translate.ipynb ](./translate.ipynb) Chinese translation to English
- [ codeai.ipynb ](./codeai.ipynb) code is automatically generated
 
PS: The graphic part of this article contains some age-restricted vocabulary due to "real-world reasons", and it is recommended that minors read it accompanied by a guardian.
 
As far as the current node (2023.02.22) is concerned, although I have studied traditional machine learning for a period of time, I am not good at deep learning and other fields, so I am not good at many words related to the AI ​​​​field, so I just summarize it for myself , so that you can update your understanding in the future.
 
The content is mainly based on the programming, writing, and painting that I was good at in the past:
 
1. Painting: text 2 image. Combining Stable Diffusion to tell the evolution of a picture.
2. Writing: chat 2 article. Combining ChatGPT to tell about content creation around specific topics.
3. Programming: comment 2 code. How incorporating GitHub Copilot can speed up everyday programming activities.
 
Generally speaking, **AI is equivalent to the strength of Captain America. If it is strong, it will be strong, and if it is weak, it will be weak** . The key lies in Prompt. Therefore, how to better improve the prompt and realize the prompt project is: the basis of how to better use AI.
 
> Prompt is a text input method for interacting with natural language processing models such as GPT. Prompt is a phrase or sentence that starts the model and produces output related to the prompt. This output can be a single word, a sentence, or a complete paragraph. It can control the behavior of the model so that it produces specific results.
Therefore, how to better improve the prompt and realize the prompt project is: the basis of how to better use AI. So, in this article, I will introduce:
 
1. Use text 2 image to show how to evolve prompt
2. Use text 2 article to show the advantages of sufficient prompt
3. Combining GitHub Copliot to implement prompt to complete the work
 
PS: Thanks to my wife for the photo.
 
##  Graph Generation: How to describe a photo? ?
 
Humans need to think about the first question: how to describe a photo? Without caring about feelings, we focus on the subject, background, color, composition, etc.
 
Now, a scenario pops up in our mind:
 
![](./output/sample.jpg)
 
Next, abstract it with text. Here, I will describe the process in conjunction with Stable Diffusion.
 
###  Text description: first example
 
Generate prompts:
 
- phodal: I want to write a paragraph describing a photo, help me beautify it: a young woman in a dress, with her back to the camera, watching the sunset by the sea, the sun is below the horizon, her hair is blowing in the wind.
- ChatGPT: The scene in this photo is mesmerizing, a young woman wearing a dress, standing by the sea, with her back to the camera, gazing at the sunset below the horizon. The sun had sunk into the sea, and a golden light diffused across the sea, illuminating the entire ocean, as if this moment was frozen in a certain corner of time. The woman's hair fluttered gently with the breeze, and the outline was soft and warm reflected by the afterglow. Her eyes stared into the distance, as if thinking about the meaning of life and the endless future. There is a profound connotation in this photo, which makes people feel the power of time and nature, and also makes people think about their role and meaning in this grand and beautiful world.
 
If converted to English:
 
> A young woman wearing a flowing dress stands at the edge of the sea, her back turned to the camera as she gazes upon
> the glow of the setting sun. The ocean stretches out before her in all its grandeur, and the sun slowly sinks below
> the horizon, casting a golden light over the water. The woman's hair sways gently in the breeze, her features softened
> by the warm hues of the sunset. Her gaze is fixed on the distance, as if pondering the meaning of life and the endless
> possibilities of the future.
After repeating N times, you will get the successful photos you want, and of course there will be failures (because there are no negative prompts configured to filter failures):
 
![ Failure ](./output/failure-seeds.jpeg)
 
However, those who are familiar with the keywords of various search engines or NLP must know that most of the above may be nonsense, which can be reduced to the following words and add some special model vocabulary, such as `black hair` , ` hand before body` , `no hand` , `bodycon dress` :
 
> women back view without face, flowing dress, edge of the sea, backview, back turned to the camera, upon the glow of the setting sun, sun below the horizon, golden light over the water, hair sways gently, Chinese style clothes, black hair,
Then, add some reverse prompts, meaning don't want these things, such as what AI is not good at: `bad hands` , `morbid` , etc. Then, constantly adjust the prompt, such as generating a better prompt:
 
<table>
<tr>
<td><img src="./output/women-backview-1.jpeg" width="256px" height="384px"></td>
<td><img src="./output/women-backview-3.jpeg" width="256px" height="384px"></td>
<td><img src="./output/women-backview-4.jpeg" width="256px" height="384px"></td>
</tr>
</table>
 
 
Such as using [ Magic Prompt ](https://huggingface.co/spaces/Gustavosta/MagicPrompt-Stable-Diffusion).
 
###  Precise map control: combined with ControlNet
 
Since the generated poses are random and uncontrollable, I introduced the ControlNet plug-in to achieve bone binding, precise control of lines, coloring of line drawings, accurate redrawing based on perspective of depth map structure, etc. Now, we can combine our creations to improve the generated graphics, such as drawing a sketch, or inputting an original picture, to generate our expected effect:
 
Finally, the resulting image is as follows:
 
![ Openpose ](output/image-with-hed.png)
 
When I finished writing the article, I modified the prompt again:
 
> women back view without face standing on the sandy beach, bodycov full skirt, edge of the sea, back turned to the camera, upon the glow of the setting sun, black hair, sunset red to blue gradient sky
The corresponding negative prompt is:
 
 
> (((simple background))),monochrome ,lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer digits, cropped, worst quality, low quality, normal quality, jpeg artifacts, signature, watermark , username, blurry, lowres, bad anatomy, bad hands, text, error, extra digit, fewer digits, cropped, worst quality, low quality, normal quality, jpeg artifacts, signature, watermark, username, blurry, ugly, pregnant, vore ,duplicate,morbid,mut ilated,tran sexual,hermaphrodite,long neck,mutated hands,poorly drawn hands,poorly drawn face,mutation,deformed,blurry,bad anatomy,bad proportions,malformed limbs,extra limbs,cloned face,disfigured, gross proportions, (((missing arms))),(((missing legs))), (((extra arms))),(((extra legs))),pubic hair, plump,bad legs,error legs, username, blurry, bad feet
The effect is improvised, which is still good. Then, we can make more attempts and adjust the parameters (commonly known as alchemy):
 
<table>
<tr>
<td><img src="./output/samples/01.jpeg" width="256px" height="384px"></td>
<td><img src="./output/samples/02.jpeg" width="256px" height="384px"></td>
<td><img src="./output/samples/04.jpeg" width="256px" height="384px"></td>
</tr>
<tr>
<td><img src="./output/samples/05.jpeg" width="256px" height="384px"></td>
<td><img src="./output/samples/06.jpeg" width="256px" height="384px"></td>
<td><img src="./output/samples/08.jpeg" width="256px" height="384px"></td>
</tr>
</table>
 
It can also be combined with inpaint to repair the distorted part.
 
###  More model sets: photos with the second dimension world (18 banned)
 
As we all know, the quality of AI generation is closely related to the model, so good quality requires a good model.
 
We can find more models on [ https://civitai.com/](https://civitai.com/ ), but because of age restrictions and other reasons, it is only recommended that you open it in a safe place, not in public The venue is open.
 
Real characters Due to various reasons of copyright, this software is quite popular in the two-dimensional world. The following are common prompt words to describe the quality of the model, which may contain some uncomfortable words. In order to reflect the real world, it is not intended to be blocked here.
 
Prompt words:
 
> modelshoot style, (wavy blue hair), ((half body portrait)), ((showing boobs, giant boobs, humongous breasts)), ((
> beautiful light makeup female sorceress in majestic blue dress)), photo realistic game cg, 8k, epic, (blue diamond
> necklace hyper intricate fine detail), symetrical features, joyful, majestic oil painting by Mikhail Vrubel, Atey
> Ghailan, by Jeremy Mann, Greg Manchess, WLOP, Charlie Bowater, trending on ArtStation, trending on CGSociety, Intricate,
> High Detail, Sharp focus, dramatic, photorealistic, black background, epic volumetric lighting, fine details,
> illustration, (masterpiece, best quality, highres), standing in majestic castle
Negative prompts
 
> (((simple background))),monochrome ,lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer
> digits, cropped, worst quality, low quality, normal quality, jpeg artifacts, signature, watermark, username, blurry,
> lowres, bad anatomy, bad hands, text, error, extra digit, fewer digits, cropped, worst quality, low quality, normal
> quality, jpeg artifacts, signature, watermark, username, blurry, ugly, pregnant, vore, duplicate, morbid, mut ilated, tran
> nsexual, hermaphrodite,long neck,mutated hands,poorly drawn hands,poorly drawn face,mutation,deformed,blurry,bad
> anatomy, bad proportions, malformed limbs, extra limbs, cloned face, disfigured, gross proportions, (((missing arms))),(((
> missing legs))), (((extra arms))),(((extra legs))),public hair, plump,bad legs,error legs,username,blurry,bad feet,
> lowres, bad anatomy, bad hands, text, error, missing fingers, extra digit, fewer digits, cropped, worst quality, low
> quality, normal quality, jpeg artifacts, signature, watermark, username, blurry
A rich enough description can help AI understand and describe our needs:
 
![ Better Quality ](./output/better.jpeg)
 
The picture above is generated by AI, and it is also the result of unblocking in the same scene - the reason is that most of the model libraries have added a lot of 18 forbidden content.
 
###  Summary
 
Now, let's think about how to describe a picture with people:
 
- Detailed descriptors.
- Pose of the character.
- Abundant models.
- Parameters that are repeatedly modified.
- Continue to iterate. (modified based on inpaint, etc.)
 
So, what about articles?
 
##  Article: How to think around a specific topic?
 
Combining the previous experience of countless failures of Stable Diffusion, we should first find a suitable framework to run ChatGPT.
 
When writing content, we will have various ideas and principles: STAR, pyramid principle, 5W1H and so on.
 
We can use STAR (Situation (situation) Task (task), Action (action) and Result (result)) as the basis for conversation with ChatGPT:
 
1. Describe a situation or background that gives the reader a better understanding of the problem.
2. State the task or goal and tell the reader what needs to be accomplished.
3. Describe the actions you took, such as what methods, tools, strategies, etc. were used.
4. Explain the results, including challenges encountered and results achieved.
 
In this way, it will help us to expand our thinking.
 
###  Situation: How to write an article with ChatGPT, How to write an article with ChatGPT?
 
phodal: I want to write an article, the topic is "How to write an article with ChatGPT, how to write an article with ChatGPT"
 
Example:
 
![](./output/chatgpt-writing-article.png)
 
However, such content is not what we want.
 
In this title, in fact, ChatGPT has already understood, how to write an article, if it is an unpopular topic, he does not know. At this point, we need to build a richer context:
 
![ focus-driven ](images/focus-driven.png)
 
At this time, the steps given by ChatGPT are still wrong, and we need to continue to correct them. So, we can consider giving a complete context at the beginning:
 
###  Build a more complete context
 
For ChatGPT, we need a clear prompt::
 
```
I want to write an article, the topic is "How to write an article with ChatGPT, how to write an article with ChatGPT", the outline of the article is:
1. First introduce ChatGPT in 100 words
2. Take Julia as an example to introduce how to use ChatGPT to write an entry for a blog contest. This includes how to decide on a topic, how to write an opening and closing, how to structure your essay, and more. The topic is: "Use of Julia Dataframe in the Field of Big Data Analysis", the outline includes: 200 words to introduce the history of Julia language; introduce how to use DataFrames.jl, and have a code example; compare Python Pandas and Apache Spark Dataframe; summary.
3. Summarize the content of this article and re-emphasize the benefits of using ChatGPT for writing.
Write an article for me?
```
 
In this way, the context we provide will be more accurate, you can see an example:
 
![ Demo ](images/chatgpt-article-demo.png)
 
Based on this paradigm, it is possible to think about how our content is written.
 
###  Build framework (frameworks)
 
ChatGPT itself builds a framework that we can then input into a useful framework to build simple feedback loops. So, I started to teach him DDD, and then learn from each other:
 
![ DDD Copilot ](images/ddd-copilot-1.png)
 
However, ChatGPT, like the image above, often loses some context.
 
phodal: In this TicketOrder aggregation, which APIs should it contain?
 
In the TicketOrder aggregation, the following APIs can be included:
 
1. createOrder(): Create a new order, which can receive parameters such as customer information, event information, and seat information, and return a unique order number.
2. cancelOrder(orderId): To cancel an order, you need to provide the order number.
3. getOrder(orderId): To get the detailed information of an order, you need to provide the order number.
4. reserveSeats(showTimeId, seatIds): To reserve seats in a session, you need to provide the session number and seat number.
5. confirmOrder(orderId): Confirm the order, the seat is locked and the order status is changed to confirmed.
6. payOrder(orderId, paymentInfo): To pay an order, you need to provide the order number and payment information.
7. refundOrder(orderId): To refund a ticket, the order number is required and can only be done when the order status is confirmed.
8. updateOrder(orderId, updateInfo): To modify order information, you can update customer information, event information, seat information, etc., and you need to provide the order number and update content.
 
The basic API can meet the needs of movie theater booking business, but the specific implementation needs to be refined and adjusted according to business scenarios and needs.
 
###  Other tips:
 
Similarly, similar to Stable Diffusion, AI-generated content often has various problems, so we should pay attention to:
 
1. Keep your expression natural. ChatGPT is able to generate fluent sentences, but sometimes strange or inappropriate expressions may appear. When using ChatGPT to write, you need to pay attention to maintaining a natural expression.
2. Correct errors in a timely manner. If the content generated by ChatGPT is inaccurate or has errors, it should be corrected in time to ensure the accuracy and readability of the article.
3. Multiple revisions and adjustments. Although the output results of ChatGPT will automatically perform grammatical error correction and editing, in order to ensure the quality of the article, it still needs to be revised and adjusted many times to continuously improve the structure and content of the article.
4. Keep it simple and clear. When using ChatGPT to write, you need to keep it as concise as possible and avoid using overly complicated sentence patterns and vocabulary, so that readers can better understand the content of the article.
5. Focus on originality and uniqueness. Although ChatGPT can generate a large number of articles, in order to stand out in the blog contest, it is necessary to pay attention to the originality and uniqueness of the articles, and to highlight one's own style and ideas as much as possible.
 
Considering that ChatGPT's code is not that accurate, let's use GitHub Copilot to generate more content.
 
##  Code Generation: GitHub Copilot
 
GitHub Copilot is an AI code generation tool launched by GitHub in August 2021, which can generate more code based on your code.
 
![ Samples ](images/github-copilot-1.png)
 
So, for Markdown itself, it can also provide some help. Of course, it is not as powerful as ChatGPT in this direction, and there are often some strange duplicate codes.
 
However, it is not unavailable, we can use it to generate some code snippets so that we can modify them.
 
###  Complete example: DDD + ChatGPT + Copilot
 
For example, combined with Chat GPT, we can complete the pre-design of the code (of course, some are unreliable):
 
![ ChatGPT DDD ](images/chatgpt-ddd.png)
 
Copy the generated API, write a line comment to tell Copilot: `convert to markdown table` , and then we have:
 
| API | Description | HTTP Method | URL | Parameters | Return Value |
|--------|----------------|--------|-------------- ----------------------------------|-------|------- ------|
| Create order | Create a new order | POST | /ticket-orders | Create order information | Order ID |
| Query order | Query an existing order | GET | /ticket-orders/{orderId} | order ID | order information |
| Cancel order | Cancel an existing order | DELETE | /ticket-orders/{orderId} | Order ID | Cancellation success or failure information |
| Add Seats | Add Seats to an Existing Order | POST | /ticket-orders/{orderId}/seats | Seat Information | Seat addition success or failure information |
| Remove seat | Remove seat from an existing order | DELETE | /ticket-orders/{orderId}/seats/{seatId} | Seat ID | Seat removal success or failure information |
| Query Available Seats | Query Available Seats for a Movie | GET | /cinema-schedule/{scheduleId}/available-seats | Show ID | Available Seat Information |
 
Next, we can use Spring + Copilot to generate some code snippets so that we can modify them:
 
![ github-copilot Sample ](images/github-sample-2.png)
 
Where there is enough information about a class, such as, we provide a note:
 
```kotlin
@PostMapping
fun  createTicketOrder (@RequestBody ticketOrder :  TicketOrder ): String {
 // check the schedule is valid, the seats are available, then create the order
}
```
 
The code it generates will be more accurate:
 
![ GitHub sample 4 ](images/github-sample-4.png)
 
And if we add the corresponding Exception processing comment: `check the schedule is valid, the seats are available, then create the order, if the schedule is not valid, throw NotScheduleAvailableException` , the code is further transformed into:
 
```kotlin
@PostMapping
fun  createTicketOrder (@RequestBody ticketOrder :  TicketOrder ): String {
 // check the schedule is valid, the seats are available, then create the order, if the schedule is not valid, throw NotScheduleAvailableException
 // check the schedule is valid
 val schedule = cinemaScheduleService.getSchedule(ticketOrder.scheduleId)
 if (schedule ==  null ) {
 throw  NotScheduleAvailableException ()
}
 // check the seats are available
 val availableSeats = cinemaScheduleService.getAvailableSeats(ticketOrder.scheduleId)
 if ( ! availableSeats. containsAll(ticketOrder. seats)) {
 throw  NotSeatAvailableException ()
}
 // create order
 return tickerOrderApplicationService.createOrder(ticketOrder)
}
```
 
In other scenarios, if your function names and parameter names are in English, the code generated by Copilot will be more accurate:
 
![ GitHub sample 5 ](images/github-sample-5.png)
 
In the unit test scenario, Copilot is more powerful and intelligent, and it can generate more test codes based on your test codes.
 
###  Other: code generation open source model
 
I also tried Salesforce
The code model: [ https://huggingface.co/Salesforce/codegen-6B-mono](https://huggingface.co/Salesforce/codegen-6B-mono ), but can not run on my MBP, some Pity.
 
##  Summary: AI is like divination
 
You may not be able to predict what the output will be, and there will always be various surprises.
 
In fact, similar to AI's prompt: when chatting with humans, we also need to provide enough context. So, you need to take a look at ChatGPT, which doesn't always understand your context.
 
##  Others: Tucao of Macbook Pro
 
Although the Macbook Pro 2019 configured by the company has an AMD graphics card, it does not have the support of CUDA and ROCm, so it can only run with the CPU.
 
###  AI ecology is not friendly
 
Such as PyTorch, previously supported ROCm acceleration:
 
![ ROCm ](https://pytorch.org/assets/images/amd_rocm_blog.png)
 
The current version is no longer available: https://pytorch.org/get-started/locally/.
 
##  Related resources for this article
 
AI generated pictures:
 
- Stable Diffusion Webui GitHub: https://github.com/AUTOMATIC1111/stable-diffusion-webui
-General AI model community: https://huggingface.co/
- Stable Diffusion AI art model community: https://civitai.com/ (18 banned)
 
Code model related:
 
- Salesforce model: https://huggingface.co/Salesforce/codegen-6B-mono
- CarpserAI: https://huggingface.co/CarperAI/diff-codegen-6b-v2
 
ControlNet Enhancements:
 
- Model: https://huggingface.co/lllyasviel/ControlNet
- Precompiled: https://huggingface.co/kohya-ss/ControlNet-diff-modules
