Date: Fri, 17 Apr 2015 13:53:07 +0000
From: Daniel Shahaf <d.s@daniel.shahaf.name>
To: Mikael Magnusson <mikachu@gmail.com>
Cc: zsh-workers@zsh.org
Subject: Re: helper script for making ChangeLog entries
Message-ID: <20150417135307.GC2426@tarsus.local2>
X-Seq: 34912

Mikael Magnusson wrote on Wed, Dec 03, 2014 at 17:16:55 +0100:
> I got a bit tired of constructing these manually, not sure how you guys
> do it but here's my script for it.

Here's my version of this.  My workflow is as follows: first, commit the
patches to the 'master' branch (using either 'git am' or 'git apply &&
git commit --author'), then run

        % zshdev-add<TAB> 42
        % git push

where 42 is the X-Seq number.  The first command generates a ChangeLog
entry, updates the commit to include it (with 'git commit --amend'), and
updates the commit's log message to include the X-Seq number.  The
ChangeLog entry is based on the first sentence of the commit message.

If there are multiple local commits on top of origin/master, the script
will amend all local commits which haven't already been amended.

Cheers,

Daniel

P.S. I also use
        zstyle ':completion:*:-command-:*:commands' ignored-patterns zshdev-add-nnnnn-and-changelog-internal

✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂✂

Update (Nov 2015): I've now eliminated the manual "look up the X-Seq number"
step by writing zshdev-am, which automates that step.

Update (Sep 2016): Added support to zshdev-am for a "take an mbox on stdin"
workflow, as produced by `git format-patch --stdout` and by Mutt after Tagging
(selecting) several messages and Piping them to a command.
