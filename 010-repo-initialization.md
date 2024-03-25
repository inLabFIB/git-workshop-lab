# Alice: repo initialization

Our writer switches on the old computer with the intention of setting up
everything to write the story in collaboration with Bob. The first step
will be to initialize the git database.

## Lab

* Alice is going to create his own workspace:

```bash
mkdir -p alice/book
cd alice/book
```

* After doing it, she starts writing the story

```bash
cat << EOF > chapter-01.md
# Tim and the waves

Being a young boy, Tim had always been fascinated with the ocean. He would spend hours at the beach, watching the waves crash against the shore, imagining all the creatures that lived beneath the surface. One day, he decided to go for a swim, but before he knew it, he was caught in a strong current and dragged out to sea.

As the waves tossed him around, Tim struggled to stay afloat. Just when he thought he couldn't hold on any longer, a strong hand grabbed his wrist and pulled him to safety. It was a kind stranger who had noticed him struggling from the shore.

From that day forward, Tim's love for the ocean only grew stronger. But he never forgot the lesson he had learned - that sometimes, even the strongest of us need help from others to make it through the rough waters of life.
EOF
```

* Alice realizes that they will need a version control for this book, so she initializes the `git` database with

```bash
git config --global init.defaultBranch main
git init
```

* The database used by `git` is stored in the `.git` subdirectory of the managed project:

```
ls -a
ls .git
```

* After that, Alice configures the database with her identity

```bash
git config user.name Alice
git config user.email alice@example.com
```

* She wants to check if the configuration has been correctly saved:

```bash
git config --list
```

* The `config --list` command is just a convenient way of checking the configuration file in the database:

```bash
cat .git/config
```
