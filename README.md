# Subreddit Blackout Tool
A Python script for sending blackout announcement posts and automatically setting subreddits to private (or back to public) for a blackout. Based on [reddit-post-scheduler by ibid-11962](https://github.com/ibid-11962/reddit-post-scheduler).

## Features
This app is designed to be run manually. 

- Takes in a list of subreddits specified in `variables.py`.
- Asks you if you want to:
    - Post an announcement to the subreddits.
    - If you want to make the subreddits private (start blackout).
    - If you want to make the subreddits public (end blackout).
- Saves previous description, sets a temporary one, and reverts back when done.
- Ability to set a custom message for the posts.
- Options to sticky, distinguish, and lock the post (and its comment), and to set the suggested sort.

## Usage

### Setting up Reddit API Access

Go to your [app preferences](https://www.reddit.com/prefs/apps). Click the "Create app" or "Create another app" button. Fill out the form like so:

- **name:** BlackoutTool
- **App type:** Choose the **script** option
- **description:** A Python script for sending blackout announcement posts and automatically setting subreddits to private (or back to public) for a blackout.
- **about url:** [https://github.com/DerfJagged/subreddit-blackout-tool/](https://github.com/DerfJagged/subreddit-blackout-tool/)
- **redirect url:** http://localhost:8080

Hit the "create app" button. Make note of the client ID (under "personal use script") and client secret ("secret").
Edit the beginning of `variables.py` to include your username, password, client ID, and client secret. Optionally, set up another account and make it a developer and a moderator of the desired subreddits if you don't want to use your own account - though it runs the risk of the reddit site filter removing posts from new accounts.

### Configuring

Edit `variables.py` and change as necessary.

The following properties are required depending on the type of posts.

- `title` Title of the post. Your subreddit name will be added to the front of it.
- `text` The body text. Required for all text posts (but not for a link-only post).
- `link` The url of the link. Required for all link posts.

The following properties are optional strings.

- `flairid` The uuid of the flair you want to use.
- `flairtext` The text of the flair you want to use.
- `collectionid` The uuid of the collection you want to post to.

The following properties are also optional, but take booleans, not strings. These all default to False, so only include them if setting to True. Some need moderator permissions. 

- `dontnotify` Disable inbox notifications.
- `lock`  Lock post.
- `distinguish` Distinguish post.
- `sticky` Sticky post.

## Running from pythonanywhere

If you do not have a server to run the script on, you can use pythonanywhere to run it for free.

- Make an account at https://www.pythonanywhere.com
- Naigate to the "Files" page.
- Click "Upload a File", and upload `blackout.py` and `variables.py`.
- Click on "Open Bash console here" and wait for the console to finish initilizing.
- Type in `python3 -m pip install praw -U --user`.
- Type in `python3 blackout.py` to run the script.
