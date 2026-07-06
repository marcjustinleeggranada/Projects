<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a Spotify Clone with Cursor

**Project Link:** [View Project](http://nextwork.ai/projects/ai-workspace-cursor)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-workspace-cursor_s2q3upload)

---

## Introducing Today's Project!

In this project, I'm going to build a queue feature for a Spotify clone web application. This will help me learn how to use the Cursor IDE, navigate a new codebase with AI, and optimize indexing using .cursorignore files. I'm interested in this because I want to master AI-assisted development to build and ship clean web applications much faster.

### Key tools and concepts

The tools I used were the Cursor IDE, Cursor Agent, Git, and GitHub to clone and run the Spotify clone repository locally. Key concepts I learnt include understanding AI context windows to get more precise code suggestions, utilizing multimodal capabilities to debug UI layout bugs with screenshots, and writing custom .cursorignore and .cursorindexingignore files to optimize the editor's indexing performance and protect sensitive keys.

### Personal reflection

This project took me approximately 60 minutes. The most challenging part was troubleshooting the missing Add to Queue button and resolving the visual dashboard rendering regressions inside our React components using Cursor's AI chat. It was most rewarding to see the sliding vertical queue panel slide in from the right and successfully update, reorder, and remove songs in real-time, showing how quickly we can build features with AI-assisted development.

### Why I did this project

I did this project today because I wanted to gain hands-on experience using an AI-native IDE to accelerate my frontend development workflows. This project met my goals by showing me how to leverage Cursor Agent to automatically build and debug interactive React components, helping me master AI-assisted development so I can build and ship clean web applications much faster.

---

## Setting Up the Cursor IDE

In this step, I'm going to download and install the Cursor IDE and create a personal Cursor account. Doing this will prepare my local development environment with an AI-powered editor so I can use its built-in AI chat features to easily manage, write, and debug the codebase for our Spotify clone.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-workspace-cursor_s1q2upload)

### How Cursor differs from other AI coding tools

Cursor is an AI-native IDE built directly on top of VS Code. It stands out because, unlike extension-based tools like GitHub Copilot that add AI features on top of an existing editor, Cursor integrates the editor and its AI chat out of the box. This allows you to read, write, edit, and auto-generate code smoothly in one unified window without having to switch between different apps or run separate terminal agents.

### Getting the starter code

In this step, I'm going to install Git and clone the boilerplate repository from GitHub because having the starter files locally on my machine is required before I can run the development server and begin building the queue feature using Cursor.

### Cloning the project from GitHub

Running the Git Clone command downloads a complete, identical copy of a remote project repository from GitHub to your local computer. This sets up all the source files, folders, and version history in a local directory, allowing you to open and edit the code inside Cursor and manage your changes using Git.

---

## Exploring the Codebase with AI

In this step, I'm going to use Cursor's AI chat to explore the folder structure of our Spotify clone and learn about AI context windows because understanding how the editor indexes my codebase will help me write better prompts when we implement the queue feature.

### The NextSound web app

This web app lets users browse and discover tracks, albums, and artists using a platform called NextSound. Built with React and TypeScript, the application can fetch live music data using Spotify's API through an Express proxy, or run offline using pre-configured mock data. It also features a searchable command palette, interactive album grids, an integrated mini audio player, and light and dark themes.

### Running the app locally

In this step, I'm going to install the required project dependencies and start our local application because installing the necessary packages with npm install ensures our code has all the libraries it needs to run, and launching the development server will let us view and test our Spotify clone live in the browser using Cursor.

---

## Creating a Brand New Feature

In this step, I'm going to plan our new queue feature in Ask mode and then implement it using the Cursor Agent because creating a blueprint first ensures the AI understands my specific requirements, and using the agent allows me to automatically write and integrate the React code needed to manage upcoming songs.

### Prompting Cursor

The key requirements in my prompt were to add an "Add to Queue" button to individual song tiles, trigger a vertical queue panel sliding in from the right, show the currently playing song prominently, enable reordering and removing of songs, keep the design non-intrusive, and strictly stick to dependencies inside package.json.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-workspace-cursor_s4q5upload)

### Designing the Queue feature

To build a new queue feature, I prompted Cursor Agent to read our plan and automatically implement a sliding sidebar panel that lists our upcoming tracks. The agent successfully modified our React components to add "Add to Queue" buttons to individual song cards, display the active track prominently, and allow users to dynamically remove or reorder songs in the queue while staying strictly within our package.json dependencies.

### Troubleshooting and iterating

In this step, I'm going to troubleshoot, debug, and refine our newly built playlist queue using Cursor's AI chat and screenshots because this will help me fix any console errors, resolve visual layout issues using the editor's multimodal AI capabilities, and ensure the entire queue feature works smoothly end-to-end.

### Debugging with Cursor

I ran into issues where the Add to Queue button was missing, the search functionality stopped working, and the main dashboard disappeared. I troubleshot this by opening Cursor's AI chat, describing the exact visual and functional bugs, and asking the AI to inspect our active files to locate the regressions. By instructing Cursor to systematically resolve the conflicts, it fixed the layout rendering and restored all features to working order.

---

## Managing AI Context

In this secret mission, I will learn to control Cursor's context by setting up custom .cursorignore and .cursorindexingignore files inside my project. Doing this will allow me to exclude unnecessary, bulky, or sensitive files from Cursor's context index, resulting in faster and much more accurate coding suggestions from the AI chat.

![Image](http://nextwork.ai/mischievous_gray_loyal_tuke/uploads/ai-workspace-cursor_s6q4upload)

### Performance and security benefits

Managing context improves performance by excluding bulky, non-essential folders like node_modules from the codebase's embeddings index, which keeps the AI's search window focused and significantly speeds up code autocomplete and chat responses. It improves security by restricting private configurations, such as .env files containing API keys and database credentials, from being read by the model or transmitted to external servers, thereby preventing accidental leaks of sensitive credentials.

### Comparing .cursorignore and .cursorindexingignore

.cursorignore hides files and folders completely from the entire Cursor editor, making them invisible in your sidebar, global searches, and all AI operations, while .cursorindexingignore only excludes files from being indexed into the AI's background codebase embeddings, meaning they are still visible in your file tree and can still be opened, edited, or manually added to the AI chat context.

---

---
