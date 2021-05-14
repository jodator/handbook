# Encodings

## Membership Metadata

| Field | Type | Label | Description |
| :--- | :--- | :--- | :--- |
| name | string | optional | Member's real name |
| avatar\_uri | string | optional | Member's avatar image uri |
| about | string | optional | Member's md-formatted about text |

## Working Group Status

| Field | Type | Label | Description |
| :--- | :--- | :--- | :--- |
| description | string | optional | Full status description \(md-formatted\) |
| about | string | optional | Status about text \(md-formatted\) |
| status | string | optional | The status itself \(expected to be 1-3 words\) |
| status\_message | string | optional | Short status message |

## Working Group Opening Description

| Field | Type | Label | Description |
| :--- | :--- | :--- | :--- |
| short\_description | string | required | Short description of the opening |
| description | string | required | Full description of the opening |
| hiring\_limit | uint32 | required | Expected number of hired applicants |
| expected\_ending\_timestamp | uint64 | required | Expected time when the opening will close \(Unix timestamp\) |
| application\_details | string | required | Md-formatted text explaining the application process |
| application\_form\_questions | [ApplicationFormQuestion](encodings.md#applicationformquestion) | repeated | List of questions that should be answered during application |

### ApplicationFormQuestion

| Field | Type | Label | Description |
| :--- | :--- | :--- | :--- |
| question | string | required | The question itself \(ie. "What is your name?""\) |
| type | [InputType](encodings.md#inputtype) | required | Suggested type of the UI answer input |

### InputType

| Name | Number | Description |
| :--- | :--- | :--- |
| TEXT | 1 |  |
| TEXTAREA | 2 |  |

## Working Group Application Description

| Field | Type | Label | Description |
| :--- | :--- | :--- | :--- |
| answers | string | repeated | List of answers to opening application form questions |

## Council Candidacy Note

| Field | Type | Label | Description |
| :--- | :--- | :--- | :--- |
| header | string | optional | Candidacy header text |
| bullet\_points | string | repeated | Candidate program in form of bullet points |
| banner\_image\_uri | string | optional | Image uri of candidate's banner |
| description | string | optional | Candidacy description \(md-formatted\) |

