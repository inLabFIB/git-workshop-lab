# Alice: moving through the timeline

**Note**: this section of the course requires root access to install a tool. If it is not possible for you to get elevated privileges, just check if `delta` is already present in the system.

## Lab

* Alice decides that a more fancy diff tool would provide better feedback, so she configures the [delta](https://github.com/dandavison/delta) diff tool:

```optional
wget -O delta.tar.gz https://github.com/dandavison/delta/releases/download/0.15.0/delta-0.15.0-x86_64-unknown-linux-musl.tar.gz
tar -xvf delta.tar.gz
mkdir -p $HOME/.local/bin
cp delta-0.15.0-x86_64-unknown-linux-musl/delta $HOME/.local/bin/delta
export PATH="$HOME/.local/bin:$PATH"
delta --version
rm -rf delta.tar.gz delta-0.15.0-x86_64-unknown-linux-musl/
```

* Now she needs to instruct `git` to make use of the new tool, by altering the configuration:

```bash
git config core.pager delta
git config interactive.diffFilter "delta --color-only"
git config delta.navigate true
git config delta.light false  # or true!
git config delta.side-by-side true
git config delta.line-numbers true
git config merge.conflictstyle diff3
git config diff.colorMoved default
```

<details>
<summary>
Now it is possible to compare again the working area version of the chapter with the first one, getting a more visual output:

```bash
git diff HEAD█:chapter-01.md chapter-01.md
```

</summary>

---
#### Solution

```bash
git diff HEAD~:chapter-01.md chapter-01.md
```
---
</details>

After comparing the two version, Alice thinks that maybe it would be more interesting to leave the future of Tim to the imagination of the reader, so he goes back in time to the previous revision

* She checks the current state of the working area and the value of the *HEAD* reference

```bash
cat chapter-01.md
cat .git/HEAD
cat .git/refs/heads/main
```

<details>
<summary>
And she compares it with the previous state, getting the SHA-1 of the first revision and using it to retrieve the original version of the chapter

```bash
git rev-parse HEAD~
PREV_REVISION=$(git rev-parse HEAD~)
git c███████ $PREV_REVISION  # Move the value of the HEAD ref
```
</summary>

---
#### Solution

```bash
git rev-parse HEAD~
PREV_REVISION=$(git rev-parse HEAD~)
git checkout $PREV_REVISION
```
---
</details>

* Wait... what does it means with *detached HEAD state*? Alice compares the current HEAD value with the one stored in *main*, to check how the first one is not pointing to the second anymore

```bash
cat .git/HEAD                  # Detached!
cat .git/refs/heads/main       # main is in the future
```

<details>
<summary>
In any case, the repo has traveled back in time as it shows the command to show the history of the changes, and the new content of the file: 

```bash
git ███
cat chapter-01.md
```
</summary>

---
#### Solution

```bash
git log
cat chapter-01.md
```
---
</details>

<details>
<summary>
Nah, Alice decides that it was not a good idea: Tim  has to have a particular background for this story to work. So Alice reverses the time traveling moving *HEAD* to the end of the line, but just for fun, she will not use the `checkout` command to do it, but an equivalent specific for branches:

```bash
git sw████ -
git log
cat chapter-01.md
cat .git/HEAD
```
</summary>

---
#### Solution

```bash
git switch - # Switch to the previously checkout branch
git log
cat chapter-01.md
cat .git/HEAD
```
---
</details>

