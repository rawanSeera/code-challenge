<img width="130" alt="Screenshot 2024-09-10 at 11 42 36 AM" src="https://github.com/user-attachments/assets/076ded8b-63a2-45cc-821c-ca109fc7e6a2">

## Developer Challenge
The main objective of this assignment is to assess test engineering skills.

## Requirements and Output
Navigate to https://www.almosafer.com/en and automate the **integration tests** for following APIs from the **Stays** funnel using **Rest Assured and Java** framework.

These APIs appear in the Network tab during the flow of searching a location and selecting a hotel — they are integrated and should be called in sequence (e.g. autocomplete → search → search poll → packages → packages poll).

- `GET /autocomplete`
- `POST /search/async`
- `GET /search/poll/{{sId}}`
- `POST /v2/packages`
- `GET /v2/packages/poll/{{pId}}`

**Note:** The list above contains only the resource paths. You must inspect the **Network tab** to obtain the full Base URI and necessary headers. The **token** in the request header is mandatory for all of these APIs to function properly.

### Conditions:
- Dates and other input data should be dynamic
- Reporting should be in place
- Request JSON bodies (especially for POST requests) should be generated dynamically
- Include both **positive and negative** test scenarios

### Response Validations:
Perform necessary validations on API responses such as:
- Status codes
- Response body structure
- Key/value assertions

## General Conditions:
- Use **Java** with **Rest Assured** framework
- Use **Maven** as the build tool
- Integrate tests with **JUnit**

## What We Are Looking For
A codebase we can trust! Clean practices, meaningful validations, and modular implementation.

This is testing code — a passed execution doesn't always mean the system works; it might mean the test itself needs review.

## Questions and Delivery
If you have any questions regarding this challenge, please feel free to reach out to us.

The challenge should be submitted via a link to a **public Git repository** (GitHub or Bitbucket preferred).

## Checklist
- [ ] Usage is clearly mentioned in the README file
- [ ] All listed APIs are automated
- [ ] Dynamic payloads and query parameters are used
- [ ] Token/header is handled correctly
- [ ] Reporting is integrated

## Note
Implementations focusing on **quality over feature completeness** will be highly appreciated. Don’t feel compelled to implement everything — even if the challenge is incomplete, please submit it anyway.
