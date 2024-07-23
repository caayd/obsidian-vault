
# SDLC
---

Software Development Life Cycle / System Development Life Cycle is a multi-step process composed of phases used by all-scale software firms to create high-quality software.

It provides:
- A structured and organized approach to software development
- Minimal risks and costs
- Efficient allocation and utilization of resources
- Effective management of software life cycle
- On-time delivery
- Quality Assurance and control

<u>Winston Walker Royce</u> is credited with introducing the waterfall model in his 1970 paper

## Key phases (waterfall)
---
<u>SDLC</u> consists of 7 key phases (In order):

- Planning
- Analysis
- Design
- Development
- Testing
- Implementation
- Maintenance


### Planning
---
Takes place after the stakeholder initiation or innovation of a project.

 In this phase resources such as customers, end-users and business analysts are <u>gathered</u> and the scope of the project is <u>defined</u>.

### Analysis
---
In this phase developers and managers of the project determine the feasibility of the project to further understand the scope and gain.

The Software Requirements Specification (SRS) document also gets created in this phase.

### Design
---
The design is based around the SRS document. More than one design will be proposed.

Designs are added to a Detailed Design Specification (DDS) document by junior members which is later reviewer by senior team members and stakeholders.

Designs are evaluated based on time and budget constraints, along with modularity and risk assessment.

The final product, data structures and interfaces are determined in this phase.

- <u>High Level Desgin</u> - architecture of software products
- <u>Low Level Design</u> - how every component of the architecture should work together with others. (inputs and outputs)

### Development
---
In this phase system components are built around the design and the stakeholder requirements. Preparation for integration and testing of the software system is also done.

High-level coding languages such as C++ or Python are utilized.

### Testing
---
In this phase software is tested for discrepancies and troubleshooting & bug fixing are done until product quality matches what is stated in the SRS.

System security is tested. This testing happens in <u>every phase</u>.

### Deployment
---
In this phase the initial release of the product is sent to a limited customer base in a true business environment.

Suggestions are made and applied to product based on User Acceptance Test (UAT) feedback.

Product is then released to a wider audience.

<u>Deployment Plan</u> and <u>Contingency Plan</u> are created.

<u>Implementation</u> includes user training, hardware installation, and integration of system.

### Maintenance
---
In this phase a major shar of the budget is allocated for operations and maintenance.

User satisfaction reports are generated to identify problems to be corrected in future development process.

---

## Boehm's First Law
---
According to Boehm's First Law, errors are more frequent during requirements and design activities and more expensive the later they are removed.

**FIX AS MANY ISSUES IN PRODUCT AS POSSIBLE BEFORE ITS TOO LATE**


# SDLC Models
---
There are 8 SDLC models that each consist of the 7 key phases:

## Waterfall
---
- Created by Winston W Royce, is a linear-sequential model.
- Considered the oldest structured SDLC methodology.
- Straightforward and rigid. One phase must finish before the next phase can begin.
- Each stage relies on the information obtained from the previous stage.
- Scope and cost of project <u>don't change</u>

Cons:
- Testing is done much later which could mess up the whole project and change the timeline.

## V-MODEL
---
- More rigid version of the waterfall model.
- Testing is present at <u>each development stage.</u>
- Each stage can only begin after the finish of the previous one.
- The development branch mirrors the testing branch.
- <u>Processes are interdependent.</u>

Cons:
- Easy to understand and manage, but only useful when no requirements are there for the projects.
- mainly used for smaller projects.

## AGILE (BEST)
---
- Created by 17 pioneers in software engineering in 2001.
- Is the industry standard in project development.
- Expands its influence beyond coding from ideation to customer experience.
- Delivers ongoing release cycles where testing happens at every iteration. Each cycle produces small incremental changes preventing many future issues.
- Stakeholder feedback is received at every release
- Uses scrum teams that work in short spurts of 2-4 weeks completing assigned tasks and participating in daily update meetings.

Requires a skillful and resourceful team. User feedback has to be clear to insure right direction of development..

## LEAN
---
Inspired by the manufacturing principles. The 7 principles of LEAN are:
1. Eliminating the waste
2. Fast delivery
3. Amplify learning
4. Builds quality
5. Respect teamwork
6. Delay commitment
7. optimize the whole system

Lean focuses only on the assigned task with no room for multitasking. Waste elimination is done at every corner to ensure efficiency.

## Iterative
---
- Used in NASA's mercury project in the early 1960's.
- Follows a repetitive procedure where project teams make software based on a set of requirements and they test, evaluate and figure out further requirements. This continues for each iteration until final version is ready.
- The major advantage is that there is a product created in the early stages.

Cons:
- Resources can get used up very quickly due to the many different iterations.
- Deep knowledge of the product is required of teams to divide the process into smaller chunks.

## Spiral
---
- Created by Barry Boehm in the mid-1980's.
- Doesn't follow a one-size fits all approach and blends together the best practices of other methodologies like waterfall and iterative.
- Enhancements happen at<u> each stage</u> of the SDLC.
- Has the advantage of risk mitigation as potential risks are spotted earlier on and steps are taken to remove/lessen them.

Cons:
- Only good when requirements aren't clear and complex.

## DEVOPS (MY FAVORITE)
---
- Uses philosophies of Lean and Agile SDLC methodologies.
- Developers and Operations teams work together closely, sometimes as a single team, accelerating innovation and deployment of high-quality and reliable software.
- discipline, continuous feedback and process improvement are some of the main features of DevOps.

This is the best as I would want to work with people on projects. The philosophies of Lean and Agile methods are also in play which is great as they are some of the most efficient/best ones.

## Prototype Model
---
- Outdated and very rarely used.
- End-users actively participate in creating prototypes prior to building the final product, with the prototypes serving as the requirements for the final product.
- Risks are mitigated and defects are detected earlier on.
- Since the end-users are actively involved, no misunderstanding of requirements happens.
- cost and time efficient