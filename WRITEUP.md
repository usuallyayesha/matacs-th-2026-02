1. AI vs. rules. Which steps in your flow use AI, and which are plain code or rules? Why did you
draw the line there?

I used AI to understand the brief. The process design is created in MIRO, I gave instruction and sequece on how it should be designed. The shapes and connections were created by AI. I asked AI for an overview of how the proposal rank criteria should be calculated, checked out some of the its suggestion. I rewrote and added some of my own rules into it since the one provided by AI was designed for the specific samples, I created the criterias to generalize it to the AI Triage Tool. 

2. Consistency and explainability. How do you make scores repeatable and explainable? If the
same proposals were ranked twice, would the result be the same? How would a reviewer see
why a proposal ranked where it did?

The tool uses defined scoring criteria, fixed weights, and explicit formulas to make evaluations repeatable. The weighted criteria are experience (30%), price (25%), timeline (15%), warranty (15%), and team and approach (15%). Each criterion receives a score, which is multiplied by its weight to calculate the overall score.

The same proposals should receive the same scores when the same extracted information, criteria, and scoring rules are used. Each proposal's result includes a score and a brief explanation. A reviewer can also inspect the individual criterion scores to understand how the final ranking was determined. Mandatory requirements are handled separately: proposals that fail them are marked ineligible, while proposals with insufficient information are flagged for review rather than assigned an invented score.

### Scoring Method and Results

The evaluation uses five weighted criteria:

- **Experience (30%):** Scored according to the relevant commercial installation experience.
- **Price (25%):** Calculated using the formula: `(Budget − Bid Price) / Budget × 100`, with a budget of CAD $260,000.
- **Timeline (15%):** Scored according to the proposed completion timeframe.
- **Warranty (15%):** Based on the panel and workmanship warranty scores, averaged together.
- **Team and Approach (15%):** Based on four factors: named project lead, qualified crew, safety plan, and monitoring plan, each worth 25 points.

The overall score is calculated by multiplying each criterion score by its weight and adding the results.

| Proposal | Experience | Price | Timeline | Warranty | Team & Approach | Overall Score |
|---|---:|---:|---:|---:|---:|---:|
| A | 75 | 8.46 | 80 | 100 | 100 | 66.62 |
| B | 50 | 27.12 | 90 | 85 | 50 | Ineligible |
| C | 60 | 6.15 | 60 | 100 | 75 | 54.79 |
| D | 75 | 11.15 | Not scored | 100 | 75 | Flagged |
| E | 50 | 6.73 | 60 | 100 | 100 | 55.68 |

Mandatory checks are applied before the final ranking. Proposal B is ineligible because the bidder's own Ontario electrical contractor licence is not established. Proposal D meets the mandatory checks but remains flagged because its completion timeline is undetermined.

Based on the available information, the eligible proposals with complete scores rank as follows: A first (66.62), E second (55.68), and C third (54.79). These results are repeatable when the same inputs, criteria, and scoring rules are used. Reviewers can inspect individual criterion scores and the supporting evidence to understand the result.


3. Human in the loop. Where does a person review, confirm or override the result? What gets
   logged for audit?


Human review is required when information is missing, ambiguous, or inconsistent. For example, Proposal D is flagged because its completion timeline is undetermined, while Proposal B is marked ineligible because the bidder's own Ontario electrical contractor licence is not established. A reviewer can examine the supporting proposal evidence, request clarification, and correct an evaluation when justified.

The tool should log the extracted evidence, criterion scores, final result, criteria version, and any warnings. It should also record reviewer decisions, manual overrides and their reasons, timestamps, and the identity of the person making a change. The final award decision remains with an authorized human decision-maker.

4. Changing criteria. What happens if an admin edits the criteria or weights after some proposals
have already been scored?

An admin should be able to update the criteria, scoring scales, or weights through a controlled configuration process. Before publication, the system should validate that the criteria are complete and that the weights total 100%. Each published configuration should have a version number.

Evaluations already completed should retain the criteria version used at the time, so their results do not change unexpectedly. New evaluations should use the applicable published version. If existing proposals need to be reassessed, an authorized user should initiate a new evaluation using the updated criteria, with the change and its impact recorded in the audit log.

5. Risks. What could go wrong with this tool (for example wrong extraction, made-up facts, bias,
   manipulation, cost), and how does your design guard against each one?


Risks can be reduced by requiring extracted values to include supporting evidence, validating the output against a defined structure, and using deterministic code for mandatory checks, calculations, and ranking. Instructions found inside proposals should be treated as untrusted content rather than followed. Missing information should be flagged instead of guessed, and human reviewers should verify uncertain or high-impact results. Audit logs, versioned criteria, and controlled access to proposal data would further improve accountability and security.
