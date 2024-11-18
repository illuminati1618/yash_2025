---
layout: page
title: MC 2018 Corrections
description: Thorough corrections on all of the questions I missed to improve my learning overall.
course: "compsci"
week: 13
type: tangibles
---

| **Number** | **Name**                                    | **Topic** | **Skills** |
|------------|---------------------------------------------|-----------|------------|
| Q14        | Comparing loop algorithms                   | 3.9       | 1.D        |
| Q39        | Internet open standards and protocols       | 4.1       | 5.A        |
| Q43        | Runtime of algorithm for online retailer    | 3.17      | 1.D        |
| Q50        | Searching list target                       | 3.10      | 4.B        |
| Q54        | Abstraction with procedures Square and Cube | 3.13      | 3.C        |
| Q58        | Defining Internet enabled crowdsourcing     | 5.4       | 1.C        |
| Q65        | Correcting errors in procedure Multiply     | 1.4       | 4.C        |

# Q14
![Q14.png]({{site.baseurl}}/images/Sprint3/2018mccorrections/q14.png)

*Why Option C is Correct:*
Both programs display the same number of values. Each displays 10 values because the loop condition (i > 10) stops both loops after the same number of iterations.
However, the values displayed are different.
- Program A displays 1 through 10.
- Program B displays 2 through 11.

*Why the Other Options Are Incorrect:*
Option A: "Program A and program B display identical values."
- This is incorrect because the starting and ending values differ. Program A starts at 1 and ends at 10, whereas Program B starts at 2 and ends at 11.

Option B: "Program A and program B display the same values in different orders."
- This is incorrect because both programs display values in the same order (ascending), but the actual values differ.

Option D: "Program A and program B display a different number of values."
- This is incorrect because both programs display exactly 10 values.

# Q39
![Q39.png]({{site.baseurl}}/images/Sprint3/2018mccorrections/q39.png)

*Why Option A is Correct:*
Open standards and protocols benefit Internet communication because they:
- Allow different manufacturers and developers to work together across the Internet.
- Create a more unified and functional system.

*Why the Other Options Are Incorrect:*
Option B: "Open standards and protocols provide ways for users to eliminate the latency of messages they send on the Internet."
- This is incorrect because open standards do not directly reduce or eliminate latency. 

Option C: "Open standards and protocols allow users to freely share or reuse material found on the Internet for noncommercial purposes."
- This is incorrect because open standards do not control the licensing or sharing of content on the Internet.

Option D: "Open standards and protocols prevent developers from releasing software that contains errors."
- This is incorrect because open standards do not enforce error prevention in software development.

# Q43
![Q43.png]({{site.baseurl}}/images/Sprint3/2018mccorrections/q43.png)

*Why Option A is Correct:*
- The algorithm's steps grow in the form of a polynomial with the number of items (`n²` growth rate). 

*Why the Other Options Are Incorrect:*

**Option B:**  
- Incorrect because the growth rate is quadratic (`n²`), not exponential, and thus remains efficient for practical input sizes.

**Option C:**  
- Incorrect because the problem is decidable since it's sorting.

**Option D:**  
- Incorrect because the algorithm is exact, not approximate.

