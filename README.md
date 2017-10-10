
- delete branch
- merge branch
- merge conflict
- pull
- push
- git remote change

# Today, we learn how to git around town!



## Part 0: Git this repo

You are free to peruse this repository using the web interface on which it is hosted, but if you
want to be able to mess around with it, we have to get it first!

_Getting_ this repository doesn't involve clicking any download buttons. That will download the
files in the repo, sure. But what it won't do, is get us all of the git history!

- To do that, find the clone URL on the page. Copy this!
- Then, navigate your git CLI to a nice, cozy spot in your filesystem. Anywhere you want!
- Run `git clone <URL>` where URL is what you just copied.

Then, git will start spitting out a bunch of text that looks like air-traffic controller messages
(I don't know anything about "resolving" a delta, but I certainly have flown on delta...).

This is just git showing progress on the download of all the history.

If this was successful, there should be a new folder called "git-around". Change into this
directory and run `git status`. It should display something more meaningful than
"This is not a git directory" or something like that.

You are now allowed to change the name of the folder by the way!

PS. `git status` is basically your new best friend. You will call on it __A LOT__.





## Part 0: Git yourself set up

Our current set up is fine if all you want to do all day is clone things and gander at them, but
we need to do a bit more if we want to actually __contribute__ to any of these repos.

There are many things you can configure regarding git behaviour, but the bare minimum we need to
configure is what name and email address will be stamped on all of the changes we make.

This can be accomplished with these two busy commands:

Set your name: `git config --global user.name "FIRSTNAME LASTNAME"`

Set your email: `git config --global user.email "email@emailprovider.com"`

You may be able to guess a lot just by looking at these, but they are saying
"Hey, __git__! I want to change my __config__!
I want this change to affect my commits __--global ly__, instead of just a single project.
First I am going to tell you my __user.name__, which so happens to be __FIRSTNAME LASTNAME__.
I am also going to tell you my __user.email__, which is __email@emailprovider.com__.
Please jot those down for me."

Now that we have that, we have all we need to start committing some crime- I mean, changes!



## Part 0: Fix the incorrect haiku in poem.txt

To do this, simply open up the file in a text editor (even notepad will do) and delete/modify the
parts that are incorrect.

Save the file. Now our changes made to the file should be recognized by git, though it hasn't done
anything with them yet.

You can make sure of this by running `git status`



## Part 0: Look at those changes!

So we have made some changes to a file, and we can verify that __something__ was changed according to git, but isn't there a way to see what has changed?

Yes, there is in fact! The command `git diff` will print out (or open up a little pager program) a line-by-line showcase of what is different between what your local files currently look like, and what git expects them to be based on history. 

This way, you can easily check what is different while you are working!

> ### Pro Tip!
> 
> `git diff` by default shows differences on a line-by-line basis, but sometimes you need a more fine-grained view to make sense of what has changed.
> 
> `git diff --color-words` will show differences on a word-by-word basis.
> 
> `git diff --color-words=.` will show differences on a letter-by-letter basis.
> 
> Honestly, I find myself using each of these in different scenarios as I work. If I run `git diff`, but can't interpret the output meaningfully, I will try one of the other two options to get a better feel for what I have changed.



## Part 0: Add the changes to the staging area

Now that the changes are saved, and we want to make this change part of the permanent history,
we must now `add` these changes to the staging area.

To do this, run `git add <FILEPATH>`, where filepath is the path to the file, including the name.
In this case, this will most likely look like `git add poems.txt`.

Now our changes are referenced in the staging area! You might have guessed by now, but you can also
make sure of this by running `git status`. My old friend...



## Part 0: Commit the change with a GOOD commit message

Now that we are happy with the bundle of changes we have in our staging area (yes, I know there is
only one in there right now), we can commit this to the git history, which will make it permanent,
as well as make it easy to _push_ it around later..

This can be done using the command `git commit`. This will open up a text editor interface that
will let us write the message we want this commit to be remembered by.

But what should we write? Are these commemorative messages worded like high school superlatives?
(Commits of 2017: Most likely to completely break production).

What is the point of a commit message anyway? If someone wanted to see what happened, they can just look at the commits contents, right?

Well, yes and no. Someone can easily figure out __what__ changed by looking at the commit contents, but maybe not __why__ it changed. The commit message should be a very simple explanation of why something changed that other people can read to get a good idea about the change.

Here are some basic rules to write _good_ commit messages.

  + Capitalize the subject line
  + Use the imperative mood in the subject line
  + Limit the subject line to 50 characters
  + Do not end the subject line with a period
  + Separate subject from body with a blank line (if there is a body)
  + Use the body to explain what and why vs. how
  + Wrap the body at 72 characters



## Part 0: Let's make some new poems!

Looking at all those Haiku has probably gotten everyone really excited to write some of their own...right?

For the sake of science, let's say it has. However, let's keep our poems in a separate file called `my-poems.txt`, because we don't want our artisinal, hand-crafted poems to get mixed in with those other...equally okay poems.

0. Create a new file called `my-poems.txt`
0. Open the file in a text editor
0. _Pour out your heart and soul_
0. Save your heart and soul out to the file

__PAUSE FOR EVERYONE TO SHARE THEIR POEMS__

Great job, everyone! I am really impressed with how good (most) of those were!

Of course, now we want to commit our poems into the git permanent history for this project. A sort of, proverbial poem hall-of-fame, if you will (I'd like to thank the academy).

First, let's check with our old pal `git status` to make sure git knows we created a new file! Easy peasy..



## Part 0: PANIC!

WHAT. WHY. Something is very wrong! `git status` doesn't report any new file changes! Clearly there should be. We just created a whole new file, after all.

At this point, we probably all expected `git status` to say something like, _Hey! There is a new/untracked file detected_. In most circumstances, it would indeed say something like that.

However, I must now admit to you all that I have swindled you. I knew this was going to happen.

You see, git has a feature that allows you to specify, on a per project basis, which files should __NEVER__ be scanned, or modified, by git. This list is referred to as the `.gitignore`.

Check your project folder. You should already have a file called `.gitignore`. Open it up in a text editor. It's contents should look something like the following:

    my-poems.*
    silly-pictures-of-a-cat.jpg

Drat! Whoever made this file (cough cough) has specified that, not only will files called `my-poems.txt` will not be allowed, but ANY file called `my-poems` with any file extension won't work either. 

(They have also prevented us from adding a silly cat picture, which I begrudgingly agree with. We are supposed to be working after all..)

It is unacceptable to call the file anything else, however. Obviously, we want to take credit for the lovely poems we just created. So what do we do?



## Part 0: Free my poems!

We have the ability to edit this file too, don't we? We can just remove that ignore rule.

0. Open `.gitignore` in a text editor
0. Delete the first line
0. Save it
0. Run `git status`

You should now see two things:

0. There are changes made to `.gitignore`
0. Your poems file is now being recognized

Interesting. So the file that tells git what to ignore..is also versioned in git. (INSERT INCEPTION MEME HERE)

Well, regardless, all we need to do `git add` all the things, and `git commit` all the things all in one go, right?

Well..



## Part 0: Split it up

We could do that..git certainly won't stop us. But just because we can, should we?

Making a single commit that both allows `my-poems.*` files, as well as adds a `my-poems.txt` file might seem intuitive at first, but these are actually two distinct concepts. One could reasonably done completely in isolation from another, and both changes would still maintain their identity.

As a proof of concept, let's try to write a __good__ commit message for this.

`Allow 'my-poems.*' files and add my-poems.txt`

Not too shabby. But there is one problem. and. And. AND. __AND__. Having to use the word 'and' within a commit message implies that two distinct things are being done, and as such, they should be seperate commits. Luckily git makes this pretty easy.

0. `git add .gitignore`
0. `git commit`
0. `git add my-poems.txt`
0. `git commit`

Easy!

> ### Pro Tip!

> This approach worked well when the two distinct changes were in two different files, but what if we have two distinct changes in the __same__ file?

> This is were `git add -p` comes in. This command starts an _interactive staging session_ that takes you through all of the changes in all of the tracked-files,  hunk by hunk.

> What the hunk is a heck? Well, a hunk is a __group of lines__ git thinks might be related based on proximity. It is a shortcut to (usually) save time compared to pure line-by-line staging.

> However, as part of this interactive staging, you have commands available to split hunks, skip hunks, add hunks, skip entire files, and so on.

> A full walkthrough of the options present is outside of the scope of this _adventure_, but I will outline the most important ones.

> For each hunk displayed to you, you may:

> - y - Add this hunk to the staging area and move to the next hunk
- n - Do not add this hunk to the staging area, and move to the next hunk
- s - Attempt to split this hunk into smaller hunks, and move to the first new hunk
- q - Leave the interactive mode, saving your decisions made so far

> After an interactive staging session, you are free to `git status` to make sure your changes are correct, and then `git commit`.



## Part 0: History Lesson

So, we have talked so far about moving things forward, and adding to history, but we haven't stopped yet to _appreciate_ history.

One of the powers of git is having an infinite audit trail that knows everything about a project. Surely there must be an easy way to access all of this?

There is! `git log`

The `git log` command opens up a paging program that allows you to look through every commit that has been made to this branch, from the dawn of time, up till right now. Each commit shows:

- Commit Hash
- Author Name
- Author Email
- Timestamp
- Full commit message

The newer commits are at the top, and it goes in reverse chronological order downwards.

For those who have not used a paging program like this before, the bare necessities are that __J__ moves downward and __K__ moves upward.

> ### Pro Tip!

> This is the basic usage of `git log`, but is has many useful options (which may be combined):

> - `git log --author <AUTHOR>` Only view commits by a certain author
- `git log -p` View the full diff of changes introduced for each commit
- `git log --stat` When the `-p` option is overkill, this command just shows the number of changes made to each file for each commit. 
- `git log --graph --all` Draw a graph, showing the merging and diverging branches that lead to this point in time (more on this later).



## Part 0: Check me out

Looking at the history, you might have noticed there are commits in this history that aren't yours. 

It is nice to be able to see these commits from long ago, but it would be even better if we could poke around the files that were present at that time.

Well __(spoilers)__ you can!

`git checkout` is a really powerful command, that among other things, allows you to __check out__ other commits in your project as if you were _really there_.

To do this, just run `git checkout <HASH>`, where HASH is a commit hash you saw in your log, or a branch name you know exists.

I know what you are thinking.

> I have to type this whole thing out?

Actually, no! Usually you can just type the first 5-7 characters of the hash and git will figure out which one you mean.

git will warn you about a __detached head state__. This is just a very git way of saying

> You will not be allowed to commit while you are here. You are a visitor, a time traveler, and this history has already run its course. You may look, but do not touch...

Good thing we just wanna look! You will notice that the files on your computer look different, as if you lost your changes.

__Don't Panic__!

You didn't lose anything. git has all of that stuff saved in the history. Git just doesn't want to break the illusion of time travel, so it made all of the files in the project look the way they would the moment after the commit you had chosen was made.

Once you are done looking around, you can just run `git checkout master` to hop back in your time machine to wherever the end of the master branch is at the moment, which was the branch you were comitting on earlier.



## Part 0: Prove your courage!

While poking around in the history, you may have noticed a commit that had a pretty weird message. That is no coincidence. That commit (and only that commit) contains a secret file, that contains a secret passcode.

Prove you have learned how to conquer history, and go and find that passcode!

> If you are doing this tutorial as part of a classrom environment, after finding the passcode, send your instructor a message containing the passcode, perhaps over __hangouts__ or something... Also don't try to just copy off your neighbor, because the code is really long and if you are trying to hand-type it, you will most certainly mess it up! YOU have to find it yourself :D



## Part 0: More Secrets?!

The secrets do not stop there. You have been working on the `master` branch until now, but in fact, there are other branches that have secrets as well.

Let's go get those secrets!

First run `git branch -a` to see a list of all of the branches. `master` is here, as we might expect, but there are also a bunch of branches called `remotes/origin/*`.

What are these?

Though these aren't __real__ network paths per se, you can still probably guess what they mean. `remotes` refers to git instances on other systems than your own, and `origin` refers to the specific remote you cloned this repo from.

All of the names where the `*` would be refer to branches that are on the origin git instance. There is one for `master`, one called `HEAD`, but there is also this `secrets` branch.

If we want to poke around this branch, you guessed it! We use `git checkout`.

Just run `git checkout <BRANCH NAME>` where you just put in the name of the branch, leaving off the whole `remotes/origin/` thing.

> Older versions of the git client might require you to manually specify that the branch you are attempting to checkout is actually remote, and as such, git needs to start 'tracking' the branch much like it tracks a new file.
>
> If this is the case, instead run `git checkout -t <BRANCH NAME>`

Notice when we hopped onto the `secrets` branch, we didn't get any message about _detached head state_. The reason for this is that branches __are__ allowed to have new commits appended to their history, whereas single commits can not be _appended to_ in the same way.

Here, you will find a `more-secrets.txt` file.

__HOWEVER. I DO NOT WANT YOU TO GIVE ME THE SECRET JUST YET!__

I want you to __merge__ secrets.



## Part 0: Worlds Collide

I do not want this secret to simply be handed over as part of a checkout. I want this secret to be merged into master first, then afterwards it may be read.

Merging is just the process of integrating __ALL__ of the commits of one branch into one other branch. Think of it like a library donating copies of all of its books to one other library.

Just to help visualize this

```
 _______________           COPY of history        ________________ 
| Master Branch |  <-------------<-------------< | Secrets Branch |
-----------------                                ------------------
```

To do this, first checkout the branch that will be accepting donations. In this case `master`.

Then, run `git merge <DONATING_BRANCH_NAME>` where the other branch name is the branch that will be donating copies of its history, in this case `secrets`.

And bam! Now master has a ton of new information in addition to what it already knew..right?



## Part 0: PANIC!: The Sequel

