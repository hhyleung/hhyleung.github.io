---
title: "GCFE - GIAC Forensic Examiner"
excerpt: "Review for the GIAC Certified Forensic Examiner (GCFE) certificate"
last_modified_at: 2022-08-18
stickies: true
stickies_path: "/assets/stickies/giac-forensic-examiner.png"
toc: true
toc_label: "Content"
toc_sticky: true
categories:
  - Certificates
tags:
  - Blue Team
---

## Stats
- Study time: 60 hours
- Practice tests: 118 minutes (first test) + 87 minutes (second test)
- Exam time: 114 minutes
- Result: 93 / 100 PASS

<br>

## Study resources
- FOR500 Windows Forensic Analysis: [https://www.sans.org/cyber-security-courses/windows-forensic-analysis](https://www.sans.org/cyber-security-courses/windows-forensic-analysis/)

<br>

## Review
I usually do short reviews only, but since this is my first GIAC certificate and it is such an expensive certificate that I won’t be able to afford a second shot, I think it deserves a longer review to document what worked for me to prepare for a GIAC certificate.

<br>

### Preface
I was lucky to have an employee that offered to pay both the SANS training and GIAC exam fee, which is definitely not common in Hong Kong. I went for the OnDemand course as I prefer to learn through speeded up videos to force myself to stay focused. I can’t keep up with live streams as I think instructors in general talk too slow, and I am a terrible reader that English words just come and go by my brain and never stay.

After reading loads of reviews on how to prepare for a GIAC certificate, most people mentioned that highlighting the books and making a decent index are the keys to ace the exam. I was sceptical about the first part. I always think highlighting words is more of a habit and indicator of reading stuff but has no real help in understanding and remembering the information.

I planned to go through the videos and labs, then write my own detailed notes that summarise all of the information from the books, with an index to it. I wanted to not bring the books to the exam and just rely on my notes, as I think it will be hard to bring the whole box of books to the testing centre. That was the plan, but plan changes.

<br>

### Studying
I went through the videos and understood everything quite quickly, followed by the practical labs that helped consolidate the knowledge. I kind of ignored the books when I was going through the videos and only opened them when I planned to start making my notes. It was by then that I realised that the videos did not cover everything that is required to know for the exam.

The books included many more details that the exam questions will refer to, while the videos were more like introductory videos on the topic to give you a head start on understanding the books. With that being said, reading the books word by word is a must.

I just know that it will take me ages to finish the books, and it is impossible to get my own notes done in time (I only had one week left before the exam). So I ditched the idea of making my own notes and instead went for highlighters. Yes, something that I questioned its existence, but I guess now I understand why.

The thing is, there are so many that will be asked in the exam, and a few details will most likely be missed out in my notes. Yet, it is guaranteed that all answers can be found within the provided books. I wanted to make my notes to avoid bringing all the heavy books and having the contents organised in a way that I can quickly reference them during the exam (without reading through paragraphs of words). The former is relatively unimportant, and the latter can be solved with highlighters.

While reading the books word by word, I highlighted the details by colour. I had green for tools, pink for numbers, orange for locations, and yellow for generic conceptual stuff. The goal is to spot the answer from the page right away, and the colour coded details indeed pop out quite nicely in this way.

I also tabbed the books by topics, with each section having its own coloured tabs. I started this as a backup plan. In case I could not find the keyword in the index, I could still go to the topic quickly using these tabs and go through the pages to find the answer. However, I find myself using these tabs a lot more often than using the index.

This is given that I was familiar with the contents of the book and how I divided them into different tabs. I kind of know which part of the book contains the answer I’m looking for. Flipping to that part of the book with the tabs was easier than going through the index to look up the exact page number and then flip to that page. I also find the index provided in the book to be useful. When I really have no clue which part of the book I should refer to or when I cannot find the keyword in my index, the provided index will always provide directions on getting to the right page.

![giac-forensic-examiner-1.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/giac-forensic-examiner-1.jpg)

<br>

### Indexing
I filled in my index at the same time. I have a notes column for each keyword containing details I think the exam might ask. This is to save the time of flipping to the page and looking for the highlighted answer. I have to say this definitely helped me a lot during the exam and turned out to be the main reason for me to use the index.

I happen to remember which detail I included in the index and which ones I did not. For those I did, I used the index and got the answer confirmed directly, without flipping to the page in the book. For those I did not, I went straight to the tabbed books and looked for the highlighted answers within the tabbed section.

I coloured the page numbers column according to the tabs I put on the book. The remaining columns in the row were coloured with the same categories as the highlighters (green for tools, etc). The index was sorted alphabetically and printed out, with the letters on the page written on the corner.

After using it for the first practice test, I found out that I wasted some time locating the keyword. Since, for example, keywords that started with the letter B were separated on pages 1 and 2, I find myself flipping between these two pages to locate the keyword. I then printed the index again, but for cases where the letter spans to another page, I shifted the entire letter section to a new page so it starts on a new page. This used more paper, but it was worth it. Locating keywords was much smoother when they were all on the same page.

In addition to the index, I duplicated the Windows event log ID entries and moved them to a separate document for quick reference. I considered printing the SANS posters but found out I never used them during the preparation stage, so I might as well save some paper and ink.

![giac-forensic-examiner-2.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/giac-forensic-examiner-2.jpg)

The last thing I printed out was a small timesheet. The time indicates the remaining time I have after finishing each question. I divided the questions into 5 columns, so I would know how far I am in the exam (eg question 46 means 40% done with the exam). I also coloured the cell for every 10 questions to locate the question number quickly. This timesheet was extremely useful and reassuring. I referred to it many times during the exam to ensure I was on track (or actually, ahead of time) without calculating every time. You can find the PDF version of this timesheet [here]({{ site.url }}{{ site.baseurl }}/assets/posts/giac-forensic-examiner-timesheet.pdf).

![giac-forensic-examiner-3.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/giac-forensic-examiner-3.jpg)

<br>

### Practice Tests
After all of the above, I barely had any time left. It was already midnight and the exam was scheduled in the afternoon. I have seen many reviews mentioning that the three hours exam was tight as it takes time to read the question and locate the answer in the book. I usually finish the exam under half the allowed time for all previous certificate exams. However, I thought that the GIAC certificate exam would not be the same because I rely heavily on the book.

To make sure I have enough sleep before the actual exam, I decided to do one of the practice tests only. The second practice test can be used if I unfortunately fail, or I could always give it away to someone else in need.

So I started the first practice test. Although I was mentally prepared to face 115 long questions, I still zoned out quite frequently while reading the question and had to reread them. I just cannot focus for long whenever I read, period. I never thought I would use the break time, but after getting 4 questions wrong consecutively, I decided to take a break to refresh my mind. By then, I was about halfway through the test.

I drank some water and reflected on what I could have done better. I am too used to exams that are not open-book, in which detailed factual questions (eg the exact version number of something minor) were not asked. But for GIAC certificate exams, details matter a lot (this does not mean they ask for version numbers, I just made up an example to describe the situation).

However, your brain can only remember a certain amount of details. It is unlikely to remember every single thing correctly, even though you think you can. The exam is not designed to test your memorisation either. The main point is to understand every concept taught in the course and know where to find the details in the book.

I realised that although I think I have the answer in mind, I should still double check my answer by finding the actual word in the book. I then continued the test and managed to focus as if I had just started the test.

Once I started double checking every answer I chose, it was not surprising to learn that there were a handful of answers I thought I had it, but I actually remembered wrong. Cross checking with the book saved these answers.

This realisation came a bit late, though. I had already made 8 incorrect answers because of trusting my unreliable memory, being time cautious (or maybe just lazy), and not flipping through the books.

That said, I finished the exam a lot earlier than expected (118 minutes instead of the total 180 minutes). Mostly it was because I did not refer to the books often enough. I was aiming for about 80% and was disappointed at myself for getting questions wrong consecutively just because of not being focused on reading the question. So, I was surprised by the final score.

![giac-forensic-examiner-4.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/giac-forensic-examiner-4.jpg)

By ending the test an hour earlier, I headed to bed early. I had enough time to complete the second practice test just before heading out to the testing centre.

I was not as time cautious this time. I kept in mind that I should double check almost every answer (except for conceptual questions, that understanding the concept would suffice to choose the correct answer and does not require memorisation at all). Also, I should utilise break times whenever I start to lose focus.

Although I had these in mind, I still made 5 careless mistakes that I could have gotten correct if I had the patience to flip through the books to confirm them. Nevertheless, I scored better than the first test and surprisingly ended much earlier (87 minutes), even though I referred to the books for most of the questions.

I believe that was because my preparation allowed me to locate the answers quickly. Instead of staring at the screen while retrieving the answer from my memory, I simultaneously opened the books to locate the answer. By the time I located the answer in the book, I mostly had an answer in mind already that I could just confirm whether or not it was correct. With the confirmation, I never hesitated for another second and could submit the question immediately. That should have saved quite some time from here and there.

![giac-forensic-examiner-5.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/giac-forensic-examiner-5.jpg)

<br>

### Actual Exam
I learnt from the practice tests that I would still have spare time even if I used the books for every question. My approach was to do the exam slowly and use the books extensively. If I could not locate the answer in one go, I should skip the question and leave it until the end.

I went through the exam smoothly, did not lose focus and did not need the break time. By the end of the exam question set, I had 90 minutes left with 9 skipped questions. In other words, I had about 10 minutes for each skipped question that I could use to read the books. That was a lot of time.

For each skipped question, I used the tabs to arrive at the relevant topic, then read the pages from the beginning. I found out that these answers were something I missed out on highlighting, which was why I could not locate them at first.

Eventually, I think there was only one question that I could not find the answer within the books. I’m sure it is in there, but I just couldn’t locate it and gave up on it. I just made a guess on that question.

It took me 114 minutes to finish the exam, and I was happy with the score. I’m not the kind of person who cares too much about scores. What I care about the most is the understanding of the material. I think I understood the materials pretty well for this exam, and the score is more of a cherry on top.

![giac-forensic-examiner-6.jpg]({{ site.url }}{{ site.baseurl }}/assets/posts/giac-forensic-examiner-6.jpg)

<br>

### Wrapping Up
I find the exam pretty applicable to real life as other exams might test on memorisation while GIAC focuses on your understanding of the material. After all, you can always Google for the details during work, but you won’t be able to know what to search for if you do not understand the concepts. Do not be shame about using the books during the exam, as one can only get the exam done in time if they understood the material by heart. If not, it is practically impossible to have enough time to locate the relevant page, understand the material right away, and spot the answer.

I was too ambitious in the beginning about making my own notes. It is impossible to cover all details. Even when I opted to highlight the details, I still missed a few, and it affected my exam progress. If I relied on my notes without bringing the books, I can only imagine that the situation would appear more, and I would have no backup plans for that.

Another thing I learned is to be slow. I tend to rush through questions that I often misread one word in the answer, leading to the wrong answer as there were two similarly worded answers that meant something entirely different. If I had read the answers slowly and carefully, I would not have chosen the incorrect answer. All in all, I think the answer options are pretty distinctive in terms of the definition / concept behind them.

Overall, I enjoyed my first experience with SANS and GIAC a lot. I am definitely interested in taking more courses from SANS (as long as my employer supports it). I would also love to find a chance to get involved in a live session to have a different experience. Perhaps the work-study program would be a fruitful experience and is something I can pay out of my pocket.

<br>