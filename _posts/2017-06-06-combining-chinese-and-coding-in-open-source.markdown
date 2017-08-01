---
layout: post
title:  "Merging Two Worlds: Combining Chinese and Code in An Open Source Contribution to the Faker Gem"
date:   2017-07-17 14:30 -0600
tags:
    -chinese
    -open source
    -code
    -faker gem
---

# Merging Two Worlds: Combining Chinese and Code In An Open Source Contribution

I lived in Beijing for two years and studied Mandarin Chinese. It was an amazing and humbling experience. After a time, I used the skills I'd picked up studying Mandarin to learn to program at the Turing School of Software and Design.

As part of our final graduation requirements, we're asked to contribute to an open source project. In my research, I started exploring the Faker gem.

### Faker Gem
The Faker gem is a program that Ruby developers can add to their projects which allows them to generate "fake" data for testing and demonstration purposes.

But perhaps the best part is the wide variety of ipsems available. Developer culture loves its humorous fake examples and Faker provides. There are fake names taken from Harry Potter or Star Wars. Fake filler text full of Chuck Norris programming jokes (yea, you read that right). It adds a spark of fun to client meetings, that's for sure.

### Exploring The Gem Structure & Locales
At first, as a backend developer, I was super confused. I kept wondering, where is all the data? I'd used [hipster ipsem](https://hipsum.co/) many times, I knew they had data stored in the gem!

The first thing to know about the Faker gem is that the data is stored not in a database, but in .yml files. As I was reading through the documentation, I noticed that it was possible to set a "locale" so that Faker produced fake data in a different language, automatically translating to the other language's faker data.

Here's an example entry in the English .yml file. Note that calling name will return one of those options, combining data.
```
university:
      prefix: [The, Northern, North, Western, West, Southern, South, Eastern, East]
      suffix: [University, Institute, College, Academy]
      name:
        - "#{Name.last_name} #{University.suffix}"
        - "#{University.prefix} #{Name.last_name} #{University.suffix}"
        - "#{University.prefix} #{Name.last_name}"
        - "#{University.prefix} #{Address.state} #{University.suffix}"
```

I was intrigued. I saw the different locales .yml files. I thought, they must have Chinese! And I found the file - "zh-CN.yml". What I soon realized was that the English language fake data has much more robust support than other languages. All those hipster words are stored in the en.yml file, but the Chinese language .yml didn't have a corresponding feature.

I decided to work on adding a little translation support to the Chinese locale. I looked for the test file for that locale and I found that it didn't exist. No test! Perfect. I'll write one. Inspired by the test for the Japanese locale, I wrote tests that matched the existing standard in the gem.

Then I moved on to actually improving the translation capacity.

### Adding Chinese Universities - Discovering a Bug

I started experimenting with Faker when set to the Chinese locale. When I tried out generating fake Chinese university names, I'd get things like "East 李" or "The 宁夏 College." What was going on?

It turns out that the method in the faker gem  called translate sets English as the default .yml file if the corresponding data is not available in locale specific file.

In this case, some university data didn't exist in the Chinese file, so when it went to generate, it would default to English words.

I decided to fix this and added the following to the yml file:
```
    university:
      prefix: ["东", "南", "西", "北", "东南", "东北", "西南", "西北", "中国"]
      suffix: ["理工大学", "技术大学", "艺术大学", "体育大学", "经贸大学", "农业大学", "科技大学", "大学"]
      name:
        - "#{University.prefix}#{University.suffix}"
```

This will return a fake Chinese university when Faker::University.name is called by combining a random prefix and suffix. The prefixes are cardinal directions like "North" and "Southeast" and the suffixes are industry specific university categories, like "Arts University" or "Science and Technology University."

I did a fair bit of research to make sure that these were good combinations of words to use for a fake university name. There were some decisions to make. For example, Chinese universities are more likely to be named after their province or city than their region. But the Chinese .yml file included a character after the province name that would not work in a university name. For example it contained 北京市 (lit. "Beijing City") or
福建省 (lit. "Fujian Province"). If I used the existing data, I'd be creating names like 北京市大学 ("Beijing City University") and a real Chinese university name would never have 市 "City" in the title. It would sound very weird. So it was a no go.

I decided a simple approach would be alright, and went with a similar pattern to the one used in the English .yml university file. A direction and a university category. It would read well to a Chinese speaker as a plausible but likely fake university. And that's the right balance.

### Adding Documentation

There was no documentation to write for adding this update to the Faker gem. However, I thought it might be helpful to add a short piece to the contributing markdown (as a link) that would explain how to add new translations to locales. I tried to mimic the existing contributing documentation in tone and style.

And then I submitted a [pull request](https://github.com/stympy/faker/pull/938) to the repo!
