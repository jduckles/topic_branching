This is an elaboration on the instructions at

https://github.com/datacarpentry/python-ecology-lesson/blob/gh-pages/CONTRIBUTING.md

which states

> 1. Fork the datacarpentry/lesson-name repository on GitHub.
> 2. The default branch in our lessons is gh-pages. Create a new branch for your changes. Give your branch a meaningful name, such as fixing-typos-in-shell-lesson or adding-tutorial-on-visualization.
> 3. Clone this repository and branch to work with it on your computer. git clone the repository with -b 'branch name'
> 4. Make your changes, commit them, and push them to your repository on GitHub.

Alas, I inferred something into those -- namely merging back into gh-pages -- when I read them.  This is my clumsy attempt to illustrate the process verbosely.

# Using branches to organize pull requests

You should, by now, be familiar with simple pull requests.  One potential
feature that may surprise you is that, once you create a pull request from
a branch of a repository, _all subsequent commits to that branch will show
up in the pull request_.

To give a specific example, let's say that we just finished Software Carpentry
instructor training, and you are going to add a challenge problem to a Data
Carpentry lesson.  The first step is to fork the lesson, but then what?  You
might just make your change, commit it, and issue your pull request.  That
will work fine; if you stop with that.

However, suppose that, while reading the lesson, you notice a couple of
typographical errors, and split infinitive, and a variable name that is
incomplete, and you decide to be a good citizen and create a pull request to
tidy those up?  You go ahead and make your changes and commit them, but
then... you notice that they already show up in your outstanding pull request!

Wait, wait!  You wanted to keep those separate, so the subject of the pull
requests were accurate and each type of change could be given a pull request
of its own.  This would be easier on you, and easier on the lesson maintainer.

When you work by yourself, you can just think of 'my changes' much of the time
and you review, commit, and move on.  When there are many people working on a
project together, though, it is much more important to isolate changes into
topics so that, for example, technical changes like spelling corrections or
changing a stale URL, can be reviewed by the lesson maintainers quickly and
closed, whereas changes to content that might want more participants and
review can stay open longer and be discussed before the pull request is
accepted (or not).  That isolation of changes is best accomplished by use of
branches.

So, let's go back to start, and you've successfully forked the lesson and
cloned it to your own computer.  Before you set to work on your proposed
challenge question, you make a new branch for it.

```
$ git checkout -b challenge_question master
Switched to a new branch 'challenge_question'
```

Now, you go ahead and edit the lesson, inserting your challenge question into
the correct spot.  You commit your change, and you try

```
$ git push origin
Everything up-to-date
```

What's up with that?  You just made a change; everything is not up-to-date!
An unqualified push to origin will push the _default branch_, so you must
specify that you want to push your new branch.

```
$ git push origin challenge_question
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 504 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:carpenterbennet/topic_branching.git
 * [new branch]      challenge_question -> challenge_question
```

Looking at the GitHub site (possibly reloading the page that shows your
repository), you can now verify that your new branch arrived.  You should
note the pulldown menu for 'Branch', to the left of the 'New pull request'.
If you haven't changed branches, the Branch pull down will have Master and
a down arrow.  If you click on Master, you'll get a list of available
branches, so you can now switch to the 'challenge_question' branch.  Once
you're in that branch, you can issue your pull request to the lesson
maintainers.

Now it's time to do your civic duty and clean up those typos and grammatical
infelicities.  Back at your own computer, you should switch back to the
gh-pages branch.

```
$ git checkout gh-pages
Switched to branch 'gh-pages'
```

Now we can create a new branch for our clean-up exercise and look at our
branch collection.

```
$ git checkout -b simple_corrections
Switched to a new branch 'simple_corrections'
$ git branch
  challenge_question
  gh-pages
* simple_corrections
```

Now you can make those typographical corrections, rejoin the parts of the
infinitive, and add the missing part of the variable name.  Once you're done,
and commit, you need, again, to push this branch to GitHub.

```
$ git push origin simple_corrections
Counting objects: 4, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 530 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:carpenterbennet/topic_branching.git
 * [new branch]      simple_corrections -> simple_corrections
```

Now you can go to the GitHub website, change your branch to
'simple_corrections', and issue a pull request.  This pull request will be
separate from the pull request you issued for the Challenge question, and it
will have a different subject, which will make it easier for the maintainers
of the lesson to evaluate and respond to them separately.

If you find additional typographical or grammatical errors, it would
be appropriate to return to the 'simple_corrections' branch, make those changes
there, and commit that branch again.  That way, all the changes that fall into
the category of 'Typographical and grammatical changes' are in the same place.
