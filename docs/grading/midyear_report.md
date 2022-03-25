# Mid-Year Review

Mid-year Reviews occur once a semester; they should really be called Mid-Semester Reviewss.  In any case, they happen in the middle of when students are to be committing code; this should be a good showcase of what they've been up to throughout the semester, and a good indication of their resulting success in RCOS.

Typically, a Mid-Year Review consists simply of a list of commits.  You can copy and paste them from all of your previous status updates, or generate the list automatically by running the following command:

``git log --author <YOUR NAME OR EMAIL> | grep ^commit | sed s/"commit "/"https:\/\/github.com\/<GITHUB USERNAME>\/<GITHUB REPO NAME>\/commit\/"/``

To do so successfully, **git** and **sed** should be installed on your computer.

	Wesley Turner
	Project: unk
	Commits:

	Wesleys-MacBook-Pro-2:unk wes$ git log --author wdturner | grep ^commit | sed s/"commit "/"https:\/\/github.com\/wdturner\/unk\/commit\/"/
	https://github.com/wdturner/unk/commit/52a2634ebeb80ca75479c515ac46d3c4b4dac67d
	https://github.com/wdturner/unk/commit/d53bbdbc30a288b1180e420c7fa4b0977d119df7
	https://github.com/wdturner/unk/commit/39f1bf1d8c798d66b24f89e5f5c48bfcb9285854
	https://github.com/wdturner/unk/commit/29e1ca83cb72b35b335d936b1de49e749f56b967
	https://github.com/wdturner/unk/commit/10d93761b77d270d849e77e6cf61b652536d1bed
	https://github.com/wdturner/unk/commit/11dc61b5fde0a151e75a45d0a30e7379afcb1530
	https://github.com/wdturner/unk/commit/80f3655b201bbd684b8b019a3800f9080c0d858b
	https://github.com/wdturner/unk/commit/b7c99572e1ecc35678dea7b652bef54d38efee9a
	https://github.com/wdturner/unk/commit/573f5aba01e5bf92a8d4789e222f9c1a37dd9c39
	https://github.com/wdturner/unk/commit/863e53457a04e6039c31c2f04418924010e2cf60
	https://github.com/wdturner/unk/commit/f3ca5c93915b2238d180d34cf17c727e461399e0
	https://github.com/wdturner/unk/commit/07eeeadb87e7a32d2b02a3f9c8bd6b434ce77c70

For clarity and the sanity of RCOS leadership, please submit actual links to commits; pull requests are cool, but limit grading visibility and accessibility.  You might get points off if you include things that aren't commits.
