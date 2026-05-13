---
title: "Chapter 3: The Command Line – Your Primary Tool"
nav_order: 3
---

# Chapter 3: The Command Line – Your Primary Tool

In the previous chapter, you've logged in to LUMI. If you were successful, you can saw LUMI's login wolf, a "Did you know?" fact, and a command line prompt that looked similar to this: 

```bash
<username>@uan01:~>       
```

**Welcome to the Shell.** This is the "Command Line Interface" (CLI). It might feel like you've traveled back in time to the 1980s, but in the world of Supercomputing and AI, this is the most powerful way to work.

##  Navigation without a Mouse

When you use Windows or macOS, you see folders and icons. You double-click a folder to see what’s inside.
On LUMI, those folders and files are still there, but you are "navigating by description" rather than "navigating by sight."

**Why do we use this for AI?**
- Automation: You can write a list of commands (a script) that LUMI can follow while you are asleep. You can't "script" a mouse click easily.
- Efficiency: LUMI is optimized for math and data processing. Displaying a fancy visual desktop for thousands of users would waste massive amounts of power that should be used for your AI models instead.
- Flexibilty: Graphical interfaces are often just "wrappers" that sit on top of command-line tools. By working directly in the shell, you're removing the middleman. You gain the ability to use every piece of software in the LUMI ecosystem exactly how the developers intended, without being restricted by visual menu options. 

## 📚 Command Line Study materials 
To learn about the Command Line and the commands to use it, we recommend reading the first 4 chapters of this high-quality [Linux Command Line guide](https://ubuntu.com/tutorials/command-line-for-beginners#1-overview). 

If you are more of a visual learner or if this is your first time learning about the COmmand Line, watch this [video guide](https://www.youtube.com/watch?v=16d2lHc0Pe8).

> [!warning] There is no "Undo"
> The command line is unforgiving and does not have a "Recycle Bin" or "Revert the previous command" functionality.
> If you use the delete command (`rm`), the file is gone instantly and permanently. We must always be careful and double-check our commands before hitting Enter.

## Practice
The best way to learn after having studied some theory is to **practice**. Let's apply what you've learned in the guides in our Command Line terminal on LUMI. You can watch and repeat after this video (???) or follow these step-by-step instructions:

1. **Where am I?**
    When you log into LUMI using `ssh` as we did in Chapter 2, you end up in your user's `$HOME` directory (this is the current 'working directory'). Check it by running:

    ```bash
    pwd
    ```

    The output should be `/users/username`. This is "where you are" now. 

2. **Create a directory** and name it 'first_dir':

    ```bash
    mkdir first_dir
    ```

    If it was successful, there is no output. Check the result by **l**i**s**ting all the files and directories in the current working directory:

    ```bash
    ls
    ```

    You should see your new directory there. 

3. **Move Inside.** Change your working directory to ("step into") the new directory: 

    ```bash
    cd first_dir
    ```

4. **Create a Document.** While in the new directory, create a new text file using `nano`, a very simple text editor: 

    ```bash
    nano first_file.txt
    ```

    - Copy paste any text into it (if pressing **ctrl+V** doesn't work, try **ctrl+shift+V**). 
    - Save the file by pressing **ctrl+S**. To help you remember, "S" in this case stands for "**s**ave",
    - Exit by pressing **ctrl+X**. "X" stands for "e**x**it". 

    > [!info]
    > The command `nano <filename>` is used to open an existing file or create a new file with that name if it doesn't exist. 

5. **Look at the file:**
    ```bash
    less first_file.txt`
    ```
    
    *Press **q** to exit the less viewer.*

    > [!tip]
    > Instead of typing the whole name of an existing file (such as in step 5), you can type the first few characters of its name (such as `less fir`) and press TAB, will automatically finish the name. If there are multiple files that start with the same few characters, press TAB twice to see available options. 

6. **Upload a file**. To upload an image from your machine (PC/laptop) to LUMI, one way is to use the web interface:
    - Open [www.lumi.csc.fi](www.lumi.csc.fi) in your browser (don't close your terminal!), log in and go to `Home directory`. This is your `$HOME` user directory where we were working in the previous steps. There you should see our `first_dir` with `first_file.txt` in it.
    - Click "Upload" and upload your image to your `$HOME` directory. 

    > [!tip]
    > Another, more 'professional' way of uploading files is to use `scp` command as [described here](https://docs.lumi-supercomputer.eu/firststeps/movingdata/).

7. Open your terminal. Go back to the "parent directory" of the current working directory: 

    ```bash
    cd ..
    ```

    Now, when you're in your `$HOME` directory you should see the file that you uploaded there (Hint: use `ls` to check that it's there).

8. Let's **m**o**v**e our uploaded picture to our new directory. Substitute `<your_image.png>` with the actual name of the image and run:

    ```bash
    mv <your_image.png> first_dir
    ```

    Change your working directory to `first_dir` and list the files in it. Hint: look at steps 2 and 3.

9. Rename the new image to `renamed_image.png`. Make sure to keep the same file extension -`.png`, `.jpeg` or any other that your image has. To rename the image, you use the same `mv` command as it's basically moving the file under a new name to a new (or the same) location:

    ```bash
    mv <your_image.XXX> renamed_image.XXX
    ```

10. Great job! Now you can disconnect from LUMI by pressing **ctrl+D**. The command prompt has changed, in Linux or MacOS to `your_username_on_your_computer @ the_name_of_your_computer` or `C:\Users\Name` on Windows. This means that you're back to **your machine** in the terminal. 

You can learn more about Linux Command Line on the ['Linux basics tutorial for CSC'](https://docs.csc.fi/support/tutorials/env-guide/) page. 

## Your Command Line dheatsheet

| Command / Key | Action | Quick Note |
| :--- | :--- | :--- |
| `pwd` | **P**rint **W**orking **D**irectory | "Where am I right now?" |
| `ls` | **L**i**s**t | Show all files and folders here. |
| `mkdir <name>` | **M**ake **D**irectory | Create a new folder. |
| `cd <name>` | **C**hange **D**irectory | Enter a folder. |
| `cd ..` | Go Back | Move up to the "parent" folder. |
| `nano <file>` | Text Editor | Create or edit text files. |
| `less <file>` | View File | Read a file without editing it (press **q** to exit). |
| `mv <old> <new>` | **M**o**v**e / Rename | Move a file or change its name. |
| `TAB` | **Autocomplete** | Type a few letters and hit Tab to finish the name. |
| `Ctrl + S` | Save | Save changes in the `nano` editor. |
| `Ctrl + X` | Exit | Close the `nano` editor. |
| `Ctrl + D` | Disconnect | Logout from LUMI and return to your local machine. |

## Summary Checklist
- You know what a Command Line is and why we use it.
- You have learned the basics of the Command Line.
- You have practiced learned commands on LUMI.