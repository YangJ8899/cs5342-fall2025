<<<<<<< HEAD
# Syllabus for CS 5342

Welcome to CS 5342, Trust and Safety: Platforms, Policies, Products.  Trust and
safety is an emerging field that focuses on reducing the harm from interpersonal
abuse in digital spaces.  The abuse types involved - harassment, misinformation,
unwanted sexual content - are often "lawful but awful," requiring developers to
build their own socio-technical frameworks of what is appropriate behavior in
their platform.  In this course, we will look at digital abuse through an
analysis of historical incidents. We will study how the field developed
standards across algorithmic response, product design and manual removals.
Students will join teams to describe an emerging online abuse type, develop
appropriate moderation pipelines (e.g., using modern machine learning such as
LLMs), and detail associated policies, all in an environment mimicking the
realities seen in practice.


Classroom: Bloomberg Auditorium (B200) 

Lectures: Tu/Th 1:25 PM - 2:40 PM

Instructors: Alexios Mantzarlis (https://www.mantzarlis.com/) and Tom Ristenpart (https://rist.tech.cornell.edu)

Office hours: By appointment

TAs: Sharon Heung (ssh247@cornell.edu)

Office hours: TBA


### Course online resources

* Course website ([Github](https://github.com/tomrist/cs5342-fall2025)): This Github repository will include general information about the course and will be updated to include lecture material and slides throughout the semester.

* Course schedule ([Google spreadsheet](https://docs.google.com/spreadsheets/d/1mrZBajxnAd-2T20SQ8vEQPFe_OfJxgf3SHRs_5uJePU/edit?usp=sharing)): A preliminary schedule is available. The schedule may evolve, but we will try to stick to it particularly with respect to the homeworks.

* Course syllabus (([Google doc](https://docs.google.com/document/d/1xMR6BffgcEUlzhJFIipahGYKin4TxQrz-sS5iJycT0Q/edit?usp=sharing)): The official course syllabus, which includes more information about requirements and grading.



### Pre-requisites

Programming skills and an introductory course on discrete structures and / or algorithms (e.g., CS 2800 or CS 4820). 
Homeworks will require good comfort with javascript and C programming. We will
also have some SQL but you be able to learn what is needed. 

If you are in doubt, talk to instructor.


### Policy on Access to Harmful Content

This course will require some interaction with harmful digital content in order
to best understand the correct prevention and mitigation strategies.  We define
"harmful digital content" as websites, apps and other types of content that
engages in or encourages illegal or almost illegal behavior (e.g., sale of drugs,
glorification of terrorism, non consensual nude generators).  Here are a few
things to know and some advice to follow. University policies:
 
* Do not break any laws: Cornell University requires people who use its information technology resources to do so in a responsible manner, abiding by all applicable laws, policies, and regulations (Policy 5.1)
* Your traffic is not monitored, with exceptions: Cornell University does not monitor the content of network traffic except for legal, policy, or contractual compliance; in the case of a health or safety emergency; or for the maintenance and technical security of the network (Policy 5.9)
Advice for this course:
* Follow safety protocols: Harmful digital content is typically hosted in locations
that do not comply with the highest security protocols. Be especially careful about what you click on, do not share any personal information, and be careful about what you download / upload.
* Minimize: You should seek to minimize your time on sites that promote harmful content and behaviors, but you are allowed to visit them if it is germane to course preparation or activities (e.g. to read the Terms of Use a deepfake pornography service)
* Document: document the reason you visited any harmful sites in a logbook for your future reference. Should any flags be raised, it will be helpful to have documentation explaining behavior.
* Observe but don’t engage: For the most part, you are strongly discouraged from doing anything other than inspecting sites that might be hateful, violent, or otherwise problematic. Do not post content, share information, or otherwise use their services unless directly instructed to do so by a member of faculty
* Report unwanted behavior: If we discover unexpected harmful content on platforms where it is against policy, please report it to an instructor and or report to the developer through the feedback mechanisms available.


### Requirements

The class will involve a combination of lectures, homeworks, participation
credit, and opportunities for extra credit. You'll be graded according to the following:

| Activity | Overview | Point Values |
| :--- | :--- | :--- |
| **1: T&S Foundations** (individual) | Students will be asked to apply key T&S frameworks to hypothetical and real world examples. The assignment is composed of ten multiple choice and five 150-word answer questions. | 20% |
| **2: Policy proposal** (group) | Students will develop a policy document that describes a Trust & Safety intervention on the platform BlueSky. This will include a definition of the type of content they want to encourage or discourage, a threat modeling assessment, and a full set of prevention and mitigation measures including product design, algorithmic interventions and manual enforcement guidelines. | 30% |
| **3: Automated moderator** (group) | Students will build a labeler on BlueSky that automatically labels certain types of accounts / posts. | 30% |
| **4: Class participation** (individual) | Students will be expected to participate regularly in class, most notably by discussing assigned readings. Students will also write blurbs about their main takeaways from guest lectures. Finally, students will be assessed by their peers on their equitable contribution to the group activity. | 20% |

Grades will not be curved, so everyone could get an A in the class if
everyone does well. 

We are planning 3 larger assignments. A preliminary schedule of assignments and
due dates appear on the course schedule linked above.  Homeworks are due on the
due date by 11:59:59pm EST. You can use in total 3 late days throughout the
semester. 

The bulk of material will be delivered via lecture, as such you won't get much
out of the class if you skip lectures and won't be prepared for homeworks. We
will make slides available, but do not plan to record lectures.  

Participation scores will be based on regular participation in class
discussions, contributing blurbs about guest
lectures, and by peer review on group project contributions.





=======
# Bluesky Content Moderation - Assignment 3

## Group Information
**Group Members:**
- Yang Ji
- Alex Xiong
- Konrad Kopko
- Hanqi Guo

---

## Project Overview
This project implements an automated content moderation labeler for Bluesky that detects potential URL scam posts. The labeler uses a multi-faceted approach combining profile analysis, content analysis, and URL checking to identify suspicious posts.

---

## Files Submitted

### Core Implementation Files

#### `policy_labeler.py`
Main implementation of the scam detection labeler. Contains the `PolicyLabeler` class with the following key methods:
- `moderate_post()`: Entry point that orchestrates all checks and returns labels
- `check_profile_for_potential_scam()`: Analyzes account metrics (follower/following ratio, post count, account age indicators)
- `check_post_for_emojis()`: Detects excessive emoji usage common in spam
- `check_post_for_sus_language()`: Matches text against suspicious phrase dictionaries and counts hashtags
- `check_post_for_malicious_urls()`: Checks URLs against known phishing database
- `check_post_for_shortened_urls()`: Detects URL shorteners (bit.ly, t.me, etc.)
- `check_post_for_any_url()`: Verifies presence of URLs (requirement for flagging)
- `extract_all_urls()`: Helper method to extract URLs from both post text and Bluesky facets
- `moderate_synthetic()`: Handles synthetic test posts for evaluation

The labeler assigns points for each suspicious indicator and flags posts that score ≥5 points AND contain a URL.

### Data Files

#### `data/medium-sus-phrases.csv`
Dictionary of suspicious phrases commonly used in scams (click here, limited time, guaranteed profit, join our discord, etc.). Posts containing 3+ phrases receive maximum content score.

#### `data/malicious_phish.csv`
Database of known malicious/phishing URLs. Posts containing these URLs are immediately flagged with high confidence.

#### `data/synthetic_posts.json`
Comprehensive test dataset containing synthetic posts

Each entry includes post text, profile metrics, expected label, and explanation.

#### `data.csv`
Combined test dataset with URLs to both real Bluesky posts and synthetic test cases. Format:
```csv
URL,Labels
https://bsky.app/profile/.../post/...,["Potential URL scam post"]
SYNTHETIC_001,["Potential URL scam post"]
```

### Starter Code Files (Provided)
- `test_labeler.py`: Testing script that runs the labeler against test dataset
- `label.py`: Helper functions for post fetching and labeling
- Other utility files from the starter code

---

## Installation & Setup

### Prerequisites
- Python 3.8+
- Bluesky account credentials

### Install Dependencies
```bash
pip install atproto pandas python-dotenv emoji
```

### Environment Configuration
Create a `.env` file in the project root:
```
USERNAME=your_bluesky_handle
PW=your_bluesky_password
```

---

## How to Run Tests

### Basic Test Run
Run the labeler against all test posts (real + synthetic):
```bash
python test_labeler.py ./labeler-inputs ./test-data/data.csv
```

**Expected Output:**
```
URLs found: [...]
The labeler produced X correct labels assignments out of Y
Overall ratio of correct label assignments: 0.XX
```

## Understanding Test Results

### Scoring System
The labeler uses a point-based system:

| Check | Points Awarded |
|-------|----------------|
| **Profile Checks** | 0-10+ points |
| - Extreme following/follower ratio (≥10:1, following ≥100) | +3 |
| - High following/follower ratio (≥5:1, following ≥50) | +2 |
| - Poor follow-back ratio (<10%, following >50) | +2 |
| - Posts-to-followers ratio (≥100) | +3 |
| - Posts-to-followers ratio (≥40) | +2 |
| - Posts-to-followers ratio (≥10) | +1 |
| - High posts, very low followers (100+ posts, <5 followers) | +3 |
| **Emoji Check** | 0-2 points |
| - 5+ emojis | +2 |
| - 3-4 emojis | +1 |
| **Content Checks** | 0-3 points |
| - 3+ suspicious phrases | +3 |
| - 2 suspicious phrases | +2 |
| - 1 suspicious phrase | +1 |
| - 10+ hashtags | +3 |
| - 7-9 hashtags | +2 |
| - 4-6 hashtags | +1 |
| **URL Checks** | 0-3 points |
| - Known malicious URL | +3 |
| - Shortened URL (bit.ly, t.me, etc.) | +2 |

**Threshold:** Posts with ≥5 points AND containing a URL are labeled as "Potential URL scam post"
---

## Customization

### Adjusting Sensitivity
Edit threshold in `policy_labeler.py`:
```python
# Line ~50 in moderate_post()
if scam_checks >= 5 and has_url:  # Change 5 to 4 (more sensitive) or 6 (less sensitive)
    return [POTENTIAL_SCAM]
```

### Adding Custom Suspicious Phrases
Edit `data/medium-sus-phrases.csv`:
```csv
phrase
your_new_phrase
another_phrase
```

### Adding Known Malicious URLs
Edit `data/malicious_phish.csv`:
```csv
url
https://scam-site.com
https://phishing-example.com
```

## Adding Test Posts

### Adding Real Bluesky Posts

To add real posts from Bluesky to your test dataset:

#### Method 1: Manual Collection
1. Navigate to the post you want to test on Bluesky web interface
2. Copy the full URL (format: `https://bsky.app/profile/[handle]/post/[post_id]`)
3. Manually label the post (is it a scam or not?)
4. Add to `test_posts.csv`:
```csv
URL,Labels
https://bsky.app/profile/scammer123.bsky.social/post/abc123,["Potential URL scam post"]
https://bsky.app/profile/legituser.bsky.social/post/xyz789,[]
```

### Adding Synthetic Test Posts

Synthetic posts allow you to test specific edge cases without relying on real posts.

#### Step 1: Add to `data/synthetic_posts.json`
```json
{
  "SYNTHETIC_051": {
    "text": "Your post text here with emojis 🚀💰 and hashtags #crypto #trading",
    "profile": {
      "posts": 100,
      "followers": 50,
      "following": 200
    },
    "expected": ["Potential URL scam post"],
    "reason": "Explanation of why this should/shouldn't be flagged"
  }
}
```

#### Step 2: Add to `test_posts.csv`
```csv
URL,Labels
SYNTHETIC_051,["Potential URL scam post"]
```
---

## Project Structure
```
bluesky-assign3/
├── labeler-inputs/
│   ├── medium-sus-phrases.csv       # Suspicious phrase dictionary
│   ├── malicious_phish.csv          # Known malicious URLs
│   └── synthetic_posts.json         # Synthetic test cases
├── pylabel                     
│   ├── label.py                     # Helper functions (provided)     
│   └── policy_labeler.py            # Main labeler implementation
├── test-data                         
│   └── data.csv                     # Combined test dataset
├── test_labeler.py                  # Test runner (provided)
├── .env                             # Credentials (not committed)
├── README.md                        # This file
└── [other starter code files]
```

---
>>>>>>> myrepo/main
