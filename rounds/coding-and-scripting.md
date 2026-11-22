# The Coding and Scripting Round

The coding round in a DevOps or SRE loop usually asks for a practical program, such as a log parser or a small command-line tool. Some large companies also ask an easy to medium algorithm question. Python is the most common language, and Bash is often accepted for short tasks.

## Task types that candidates report

| Task type | Example | What it tests |
|---|---|---|
| Log parsing | Count requests per status code from an access log | File reading, string handling, dictionaries |
| Text processing | Find the 10 most frequent client addresses | Counting and sorting |
| Automation | Check 50 hosts and report those that fail a health check | Loops, timeouts, error handling |
| Small tools | Write a command that reports the largest files under a directory | Recursion or a directory walk |
| Data structures | Implement a rate limiter or a cache with a size limit | Queues, maps, time handling |
| Algorithms | Merge overlapping intervals, such as maintenance windows | Sorting and one pass |

## Worked example: a log parser

The task: "Given a web server access log, print each status code with its count, highest count first." Each line holds the status code in the ninth field when split on spaces.

```python
import sys
from collections import Counter

def count_status_codes(path):
    counts = Counter()
    with open(path) as log:
        for line in log:
            fields = line.split()
            if len(fields) < 9:
                continue  # skip a malformed line instead of failing
            counts[fields[8]] += 1
    return counts

if __name__ == "__main__":
    for status, count in count_status_codes(sys.argv[1]).most_common():
        print(status, count)
```

Three choices in this answer earn credit. The file is read one line at a time, so memory use stays constant for a file of any size. A malformed line is skipped and does not stop the program. The counting logic sits in a function, so it can be tested without a file on disk.

The same task in a shell is one line.

```bash
awk '{print $9}' access.log | sort | uniq -c | sort -rn
```

Offering both shows judgment about when a script is worth writing.

## Follow-up questions to expect

1. The file is 50 GB. Does the program still work? (Yes, because it never loads the whole file.)
2. The log is still being written. How would you process new lines as they arrive?
3. How would you count only the last 5 minutes?
4. How would you run this across 200 servers and combine the results?
5. How would you test it?

## What the interviewer listens for

- The candidate asks about input size and format before writing code.
- Errors are handled: a missing file, an empty line, a timeout.
- The program can be run again safely. A script that can be repeated without changing the result is called idempotent.
- Names are clear, and the logic is in functions.
- The candidate states the time and memory cost.

## How to prepare

| Activity | Amount |
|---|---|
| Practical scripts written from an empty file | 10 to 12 |
| Easy and medium algorithm problems | 25 to 30 |
| Timed sessions of 40 minutes, explaining aloud | 4 |

Focus the algorithm practice on arrays, strings, hash maps, queues, intervals, and trees. Graph and dynamic programming questions are reported far less often for these roles.

## Go deeper

- [Grokking DevOps and SRE Interviews](https://www.designgurus.io/course/grokking-devops-and-sre-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-coding-and-scripting) has a coding and scripting chapter with graded Python exercises built on operations tasks.
- Lesson: [What Coding Rounds Test](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/what-coding-rounds-test?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-coding-and-scripting), in Grokking DevOps and SRE Interviews
- Lesson: [Exercise: Parsing a Web Server Log](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/exercise-parsing-a-web-server-log?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-coding-and-scripting), in Grokking DevOps and SRE Interviews
- Lesson: [Bash for Interviews](https://www.designgurus.io/course-play/grokking-devops-and-sre-interviews/doc/bash-for-interviews?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-coding-and-scripting), in Grokking DevOps and SRE Interviews
- [Grokking the Coding Interview](https://www.designgurus.io/course/grokking-the-coding-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-coding-and-scripting) teaches the patterns behind the algorithm questions.
- [Is coding asked in a DevOps interview?](https://www.designgurus.io/answers/detail/is-coding-asked-in-devops-interview?utm_source=github&utm_medium=repo&utm_campaign=devops-sre-interview&utm_content=rounds-coding-and-scripting) is a longer Design Gurus answer on how much coding to expect.
