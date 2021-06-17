---
layout: post
title: "Webinar Notes // Advanced LinkedIn for OSINT Research"
date: 2021-06-15 23:00:00 +0300
tags: Webinar OSINT 
hidden: true
---

![advanced linkedin for osint research cover](/img/webinar/2021june/linkedin1.png)

## Speaker
**Irina Shamaeva** is a recognized leader in Sourcing, Social Recruiting, and Internet Research. Lately, her content has been gaining popularity in OSINT circles.

She is Partner and Chief Sourcer at [Brain Gain Recruiting](https://braingainrecruiting.com/), an executive search firm that eventually expanded into research and training.

For more information about her you can visit [her site](https://booleanstrings.com/about/) or you can follow [her twitter](https://twitter.com/braingain).

## Organizer
The organizer is a company called [Social Links](https://sociallinks.io). Their product manager Sofya Oronova talked about their product, Social Links Pro. 

You can watch their previous webinar recordings on [their youtube channel](https://www.youtube.com/channel/UCcFD986JKvXXU88w0SRfvow).

## Notes
- You can visit the speaker's website for more detailed information. I think she compiled some key points from her articles for the webinar. Also you can follow Social Links' Youtube channel to check out if they uploaded the webinar recording. 

- The main talking point was searching on LinkedIn with boolean logic.
**Operators** (All capitalized):
	- AND 
	- OR
	- NOT

- There will be some **false positives** on your search because some people forgot to "close" their previous job experiences. It looks like they are still working on their previous jobs but they don't.

- Companies on LinkedIn generally have **inflated numbers of employees** due to unclosed past positions.

- You can only search with ~5 operators but there are **workarounds**:
	- Don't use AND explicitly.
		- **DON'T:** Java AND spring AND rest AND aws AND nosql AND "elastic search" AND microservices
		- **DO:** Java spring rest aws nosql "elastic search" microservices
	- Use parenthesis when working with OR.
		- **DON'T:** Mary OR Emma OR Sophia OR Linda OR Olivia OR Emily OR Victoria OR Lisa OR Isabella
		- **DO:** Mary OR(Emma) OR(Sophia) OR(Linda) OR(Olivia) OR(Emily) OR(Victoria) OR(Lisa) OR(Isabella)
	- Use parenthesis when working with NOT.
		- **DON'T:** engineer NOT senior NOT manager NOT director NOT recruiter NOT 	cto NOT ceo
		- **DO:** engineer NOT(senior) NOT(manager) NOT(director) NOT(recruiter) NOT(cto) NOT(ceo)

- If your search includes something similar to **job titles**, LinkedIn will narrow results down to job titles including past experience and present experience and it will include similar titles.

- Boolean is **more inclusive** as opposed to selections as they will include similar texts and have tolerance to unusual spellings. 

- **Company selection** will include the acquired companies on the results. Company name search **without selection** will find the companies containing the searched companie's name.

- [Hidden search operators](https://booleanstrings.com/linkedin-search-operators/)

- Enclose **phrases** in the quotation marks.

- Do not use AND/OR/NOT in the arguments.

- **Accented characters** and letter capitalizations are ignored.

- **First and last names** are varied e.g. Geraldine will also find Gery, Gerry, Jerry, etc. 

- *title:"vice president" NOT(company:bank title:"vice president")**

- There are some **codes** to search operator values. You can find out the codes by looking at examples. For example, go to a school alumni search then select a field of study like Economics. Then you will see the Economics' code on the URL.

- For example: *companytype:C companysize:F* finds employees of public companies with 501-1000 employees. *seniority:7* finds VP-level members.

- *spokenlanguage:[language-name]* and *profilelanguage:[2-letter-language-abbreviation]*. These operators are useful in searching for **bilingual members and expats**.
	
- Combined examples:
	- (headline:"quality assurance" OR(headline:qa)) skills:"framework automation"
	- headline:"hardware engineer" endyear:2008 skills:C

- **Company size** is derived from the number of members who listed the company as employer.

- **Issues:**
	- Seniority, function values may not be what you expect.
	- Years of experience is buggy.
	- Many profiles have values that LinkedIn couldn't categorize.
	- Calculated values may be wrong.

- **Pushing the weekly invitation limit** by identifying members from a list of email addresses:
	- Check whether you have imported data (Contacts), if you do remove it.
	- Create a CSV file. Format:
		- first, last, email. first and last does not matter, can be random.
	- Upload the file to Contacts.
	- Up to 8-9k emails can work. 

- The code "A" will search for your **group members**. &network=["A"]

- **Messaging to a group member:**
	- Go to the profile and see the groups you have in common.
	- Go to the group and find the person by the name, send a message for free.
	- There is no longer a monthly limit for messages in groups.

- site:linkedin.com/in intitle:"chief financial officer"

- Use the advanced search dialog and set the country/region for **x-raying by country**.

- You can find **entries on member's public profiles** that carry images using "image for" as part of the string. *site:de.linkedin.com/in "image for Certified Information Systems Security Professional"*

- site:linkedin.com/in "image for * * activity called working from home"

![resources and q&a](/img/webinar/2021june/linkedin2.png)

## Some Questions Participants Asked
**Q.** Does this tool work on LinkedIn as well? (They talk about the browser extension Irina Shamaeva uses to scrape data.)<br>
**A.** Instant data scraper does not work on LinkedIn. You can use Data Miner or another scraper.

**Q.** What do you think about doing research on linkedin directly in Google? Could it overcome "Linkedin difficulties" in research and/or booleans? like using "site: linkedin"?<br>
**A.** Some - but there is no substitute for a filtered search.

**Q.** Do the search operators work for the Linkedin premium accounts and the accounts that with customized settings?<br>
**A.** Yes, they do.

