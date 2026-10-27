# Email Forensics: How Investigators Trace a Phishing Email

## Introduction

Email is still the most common way attackers reach their victims. A fake bank alert, a fake job offer or a message that looks like it came from your manager can all lead to stolen passwords or money. When such an email is reported, digital forensic investigators are asked a simple question: where did this message really come from?

Email forensics is the part of digital forensics that answers this question. This article explains, in simple terms, what an email contains, how investigators read it, and what limits they face.


## What Is Inside an Email

Every email has two parts. The body is the text and attachments that the reader sees. The header is a block of technical lines that travels with the message and is normally hidden. For an investigator, the header is the more valuable part, because it records the journey of the email.


## Key Header Fields

- **From:** the sender name and address shown to the reader. This is easy to fake.
- **Reply-To:** the address that receives replies. If it differs from the From address, it is a warning sign.
- **Return-Path:** the address where delivery errors are sent.
- **Message-ID:** a unique code created by the sending mail system. Odd or mismatched values can point to a forged message.
- **Received:** one line is added by every mail server that handles the message. Together they form a trail. They are read from the bottom to the top, because the oldest line is at the bottom and the newest is at the top.
- **Authentication-Results:** shows whether the email passed SPF, DKIM and DMARC checks.

## Authentication Checks

Three standards help receiving servers judge whether a sender is genuine. SPF checks whether the sending server is allowed to send mail for that domain. DKIM adds a digital signature that shows the message was not changed on the way. DMARC tells the receiver what to do when SPF or DKIM fails, such as rejecting the message or sending it to spam. A phishing email that claims to be from a bank but fails all three checks is strong evidence of spoofing.


## How Investigators Work Step by Step

**1. Preserve the evidence.** The investigator saves the original email in a format such as .eml, which keeps the full header. Forwarding the email is avoided, because forwarding changes the header. The saved file is hashed so that its integrity can be shown later.

**2. Read the header.** The Received lines are followed from bottom to top to find the first server and its IP address. The investigator also compares the From, Reply-To and Return-Path fields.

**3. Check authentication.** The SPF, DKIM and DMARC results are noted.

**4. Look up the sender details.** IP lookup and WHOIS tools show which network or hosting company owns an IP address, and when and where a domain was registered. A bank domain registered only a few days ago is very suspicious.

**5. Examine links and attachments.** Links are inspected without opening them, and attachments are checked safely, often in an isolated test environment.

**6. Document everything.** Every step, tool and result is recorded so that another examiner could repeat the work and reach the same conclusion.


## Common Tools

Many email services let users view the original message and its full header. Online header analyzers, such as the one from MXToolbox, display the hops in a readable table. Larger investigations use forensic suites such as Autopsy or FTK, which can open mailbox files and search thousands of messages at once.


## A Simple Example

Imagine an employee receives an email that appears to come from the company's finance team, asking for an urgent payment. The display name looks correct, but the investigator sees that the Reply-To address belongs to a free email service. The header shows that SPF failed, and the first Received line points to a server in a hosting network unrelated to the company. A WHOIS search shows that the domain in the link was created only two days earlier. Together, these findings show that the email was a spoofed phishing attempt, and the evidence can be passed to the security team or the police.


## Limitations

Email forensics is useful, but it is not perfect. Attackers can forge the lower Received lines to mislead investigators, so only lines added by trusted servers can be relied on. VPNs and proxy services can hide the true location of the sender. Some webmail services do not reveal the sender's own IP address. In many cases the attacker uses a hacked genuine account, which makes the email look authentic. For these reasons, investigators combine header analysis with other evidence, such as server logs, and often need legal requests to obtain records from service providers.


## Simple Tips for Everyone

Check the real sender address and not only the display name. Hover over links before clicking. Be careful with urgent requests for money or passwords. If an email looks suspicious, report it and keep the original message instead of deleting it.


## Conclusion

An email is more than the text on the screen. Its header holds a record of where the message has been, and with careful reading, authentication checks and proper documentation, investigators can often show whether it is genuine or fake. Email forensics works best when it is combined with other evidence, and its results are only as strong as the care taken in preserving the original message.

