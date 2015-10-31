# Guildline

1. master branch 只能 merge，不能直接 commit，以防止無窮無盡的 merge conflict!
(即使是再小的修正，都必須使用pull request)

  [工作守則](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)

  The Feature Branch Workflow still uses a central repository, and master still represents the official project history. But, instead of committing directly on their local master branch, developers create a new branch every time they start work on a new feature. Feature branches should have descriptive names, like animated-menu-items or issue-#1061. The idea is to give a clear, highly-focused purpose to each branch.

  Git makes no technical distinction between the master branch and feature branches, so developers can edit, stage, and commit changes to a feature branch just as they did in the Centralized Workflow.

  In addition, feature branches can (and should) be pushed to the central repository. This makes it possible to share a feature with other developers without touching any official code. Since master is the only “special” branch, storing several feature branches on the central repository doesn’t pose any problems. Of course, this is also a convenient way to back up everybody’s local commits.

2. Pull request 不能自己 merge, 需要由非作者的人去 merge

  [Pull Requests](https://www.atlassian.com/git/tutorials/comparing-workflows/feature-branch-workflow)

  Aside from isolating feature development, branches make it possible to discuss changes via pull requests. Once someone completes a feature, they don’t immediately merge it into master. Instead, they push the feature branch to the central server and file a pull request asking to merge their additions into master. This gives other developers an opportunity to review the changes before they become a part of the main codebase.

  Code review is a major benefit of pull requests, but they’re actually designed to be a generic way to talk about code. You can think of pull requests as a discussion dedicated to a particular branch. This means that they can also be used much earlier in the development process. For example, if a developer needs help with a particular feature, all they have to do is file a pull request. Interested parties will be notified automatically, and they’ll be able to see the question right next to the relevant commits.

  Once a pull request is accepted, the actual act of publishing a feature is much the same as in the Centralized Workflow. First, you need to make sure your local master is synchronized with the upstream master. Then, you merge the feature branch into master and push the updated master back to the central repository.

3. [Possible workflow suggestions](http://stackoverflow.com/questions/2428722/git-branch-strategy-for-small-dev-team)

  You might benefit from the workflow Scott Chacon describes in Pro Git. In this workflow, you have two branches that always exist, master and develop.

  Master represents the most stable version of your project and you only ever deploy to production from this branch.

  Develop contains changes that are in progress and may not necessarily be ready for production.

  From the develop branch, you create topic branches to work on individual features and fixes. Once your feature/fix is ready to go, you merge it into develop, at which point you can test how it interacts with other topic branches that your coworkers have merged in. Once develop is in a stable state, merge it into master. It should always be safe to deploy to production from master.

  Scott describes these long-running branches as "silos" of code, where code in a less stable branch will eventually "graduate" to one considered more stable after testing and general approval by your team.

  Step by step, your workflow under this model might look like this:

  1. You need to fix a bug.
  2. Create a branch called myfix that is based on the develop branch.
  3. Work on the bug in this topic branch until it is fixed.
  4. Merge myfix into develop. Run tests.
  5. You discover your fix conflicts with another topic branch hisfix that your coworker merged into develop while you were working on your fix.
  6. Make more changes in the myfix branch to deal with these conflicts.
  7. Merge myfix into develop and run tests again.
  8. Everything works fine. Merge develop into master.
  9. Deploy to production from master any time, because you know it's stable.

  For more details on this workflow, check out the [Branching Workflows chapter](http://git-scm.com/book/en/Git-Branching-Branching-Workflows) in Pro Git.
