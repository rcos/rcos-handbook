# New Projects

We always welcome new projects! If you want to start a project from scratch, here's how to get your project up and running.

Note that if you are an external organization or external project, these guidelines may vary.

## Forming a Team

You can work by yourself, but managing an open source project by yourself can be very difficult. We highly recommend forming a team if you don't already have one!

#### 1. How Many People?

If you are starting a brand new project, have little experience with the technologies you are choosing, and/or have little experience with project management, we heavily recommend you **keep your team small** (no more than 6-8 team members). You might think at first that more members means more work gets done, but in reality it means you spend all of your time as a Project Lead teaching and directing your project members! Or, in a worse scenario, you don't have the time and resources to dedicate to everyone and team members fall behind on work and do poorly in RCOS as a result. Note that if you find yourself with little time to write code since you are teaching and managing your team, try to turn that into contributions in the form of documentation! Reach out to your Mentor(s) for specific ideas.

- [ ] Determine the maximum number of team members you feel like you can handle

Project teams have a soft limit of 12 people and a hard limit of 16. Any teams having more than 12 people need explicit approval from the coordinators and/or faculty advisors. Any teams wishing for more than 16 participants MUST divide themselves into subteams that will act as independent teams under a multilayer management system. See below:

![large team multilayer diagram](https://github.com/rcos/rcos-handbook/blob/add-team-size-limit/docs/project_management/large_team_multilayer_diagram.png?raw=true)

#### 2. Pitch Your Idea to RCOS Community

Some Project Leads pitch their project idea via word of mouth and come up with a team that way. That works totally fine! However, if you want to pitch to the general RCOS community for members, you will participate in [Project Pitches](project_management/pitch.md) which take place in the very first few RCOS meetings of the semester. Read more about project pitches at that link.

- [ ] Determine whether to pitch or privately form team
- [ ] Create and submit Project Pitch (if pitching)

#### 3. Project Pairing

!> If you already have members committed to your project and did not pitch, you do not need to do Project Pairing.

If you have pitched your project, you will need to interact with RCOS members who are interested in potentially joining your project! This takes place in an exciting process called [Project Pairing](membership/project_pairing), which occurs immediately after project pitches at the start of the semester. You will represent your project in-person to any interested members, in a sort of speed-dating format. You will get to talk to and pitch your project to many RCOS members to determine if they are interested and a good match for your project. You must give the go-ahead to members who want to join your project, they cannot join just by requesting alone.

- [ ] Attend Project Pairing and represent your project
- [ ] Approve members to join your project

## Setup

#### 1. Writing a Project Proposal

Woo hoo! You've formed a team to work with you on your RCOS project. Before you begin contributing, it's important to set goals for the semester. After you form a team, you will have to write a Project Proposal for your project for the current semester. It's a simple document containing your project title, team members, and general milestone goals for the semester. We don't grade you based on achieving your goals, but instead encourage it to be a living document that evolves along with your project. See the [rubric](grading/documentation?id=proposal) for more details on proposals. Make sure it meets the requirements specified, as Mentors/Coordinators will be reviewing these and giving feedback before contributing starts. You'll be directed where to submit this.

- [ ] Submit Project Proposal where directed to
  - [ ] Ensure it meets the requirements

#### 2. Project Repository

Create a repository on GitHub (or similar platform) for your project. Ensure it is **PUBLICLY ACCESSIBLE** and not private. We're the center for Open Source after all! Then, create the following documentation files:

- `README` - describe your project
- `LICENSE` - choose an open source license via https://choosealicense.com/
- `CODE OF CONDUCT` _(optional but recommended)_
- `CONTRIBUTING` _(optional but recommended)_ - detail how to contribute to the codebase
- Issue/pull request templates _(optional but recommended)_

See our [documentation guide](grading/documentation) for specific guidelines. Generally, the more documentation your project has, the better experience your entire team has.

- [ ] Create **public** repository
- [ ] Give team members appropriate access
- [ ] Add required and recommended documentation

#### 3. Choose a Git Workflow

You and your team members will come from a variety of different backgrounds, including differing experience with Git. It is vital that you choose a Git workflow and explicitly document it and explain it to your team members to ensure your team can work together without the chaos and confusion of merge conflicts and branching/forking/rebasing/etc. disasters. Talk with your team to learn about their experience levels and research different workflows using resources such as [this](https://about.gitlab.com/topics/version-control/what-is-git-workflow/) to determine what will work best for everyone. Document this in the `CONTRIBUTING` file in your repository.

?> Here's an [example wiki page](https://github.com/Apexal/late/wiki/Development-Setup-Review) from a past project that details how the Project Lead wanted team members to contribute.

- [ ] Choose a [Git workflow](https://about.gitlab.com/topics/version-control/what-is-git-workflow/)
- [ ] Explicitly document it in repository to serve as a reference

#### 4. Discord channel

**You shouldn't have to do anything!** When projects are finalized, we automate the creation of categories for each Small Group which include a voice and text channel for your project. The text channel is only visible to you, your team, and the Coordinators/Faculty Advisors. You are given permission to pin and delete messages in your project's channel. Reach out to a Coordinator if you every have issues with your channel or need help.
