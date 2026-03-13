# Spring-2026_Task_1

## Part A: Implementation

In this first assignment, you will study the basics of ROS 2 and set up the environment for completing all assignments in this course.

ROS 2 — which stands for Robot Operating System 2 — is a framework (not a real operating system in the traditional sense) for implementing robotics and autonomous machine systems. It provides a decentralized architecture and a way to implement nodes, which are used to package desired features for an autonomous cyber-physical system (CPS). It also provides an open-source community that offers peer support and a forum for distributing implemented packages to others. Since we unfortunately do not have access to real robotics hardware in this course, we will use simulations instead. As a simulation environment, we will use Webots, which provides tools for assembling different types of robots and sensor systems.

In this first assignment, you will study ROS 2 basics in a way that suits you best. We have provided links to videos and online tutorials. It is also highly recommended that you use AI tools (such as Claude, ChatGPT, Gemini, Copilot, etc.) to help explain ROS 2 concepts that you want to understand better. These tools can also be very helpful if you encounter technical issues. One of the learning outcomes of this course is to learn how to use AI tools in the development of autonomous cyber-physical systems.

It is completely up to you how you choose to use AI tools. The only mandatory requirement is to report (Part B) how you used them and provide some self-reflection on your motivation for using these tools, what you learned, and how you verified that your output is correct.

After finishing your assignment, you will submit a video report describing what you implemented (Part A) and how you used AI tools (Part B). Your implementation and AI usage will then be peer-reviewed by other students (Part C).

Each part (A, B, and C) is mandatory and will affect your final grade.



## ROS2 Basics
#### ROS2 Jazzy will be used throughout the exercises.

#### The ROS2 official documentation is very good and can be your main source of learning.
- [ROS2 Jazzy Official Documentation](https://docs.ros.org/en/jazzy/index.html)

#### The following is a good tutorial series by Kevin Wood (Robotics and AI channel). Although this tutorial is for ROS2 Humble, the basic concepts are the same.
- [YouTube Tutorial](https://youtu.be/C6eQ6VwTpxk?si=884uxn9IBFt9s_Mw)


## Webots Simulator
#### The Webots simulator will be used in this course. The main purpose of choosing it is that it is lightweight, open-source, and runs on systems with low or no GPU requirements.

#### The Webots official documentation is good. Familiarize yourself with the basics of the simulator.
- [Webots Documentation](https://www.cyberbotics.com/doc/guide/index)

#### There are some YouTube tutorial series you can follow to get a quick understanding of the simulator.
- [YouTube Tutorial](https://youtu.be/luyg3plGujg?si=W8zWztR1vgbkMp-z)


#### For this task you will need to set up the environment by following the instructions below. The instructions first ask you to install Webots on your computer, and then create a Docker container with ROS2 Jazzy installed in it. The container also contains the ROS2 package for the task, which you can edit later. The purpose of the Docker container is to handle version compatibility between your OS and ROS2 Jazzy.



## How it works


```
Your computer
├── Webots  ← runs natively (full GPU, no display issues)
└── Docker container
    └── ROS2 Jazzy  ← all your code runs here
            ↕ TCP port 1234
        webots_ros2 driver bridges them
```

You write and edit code on your host machine using VS Code.
The code runs and builds inside the container.

---

#### Alternative way
If you don't want to use Docker and want to install everything directly on your computer, follow the official documentation for installing ROS2 Jazzy: [ROS2 Jazzy Official Documentation](https://docs.ros.org/en/jazzy/index.html). Then download and install [Webots](https://cyberbotics.com/) and follow this tutorial: [Webots with ROS2 Jazzy](https://docs.ros.org/en/jazzy/Tutorials/Advanced/Simulators/Webots/Simulation-Webots.html)

Notice that not all features and packages are available when running ROS 2 on macOS and Windows without virtualization.

> **Environment:** ROS2 Jazzy (Docker) + Webots (native on your OS)


---

## 1. Install prerequisites

### Webots (on your host OS — do this once)

Download and install **Webots R2025a** for your OS:
https://github.com/cyberbotics/webots/releases/tag/R2025a

| OS | File to download |
|---|---|
| Windows | `webots_2025a_setup.exe` |
| macOS | `webots_2025a.dmg` |
| Linux | `webots_2025a_amd64.deb` |

### Docker Desktop (do this once)

| OS | Instructions |
|---|---|
| Windows | Install Docker Desktop. During install ensure **"Use WSL2"** is checked. |
| macOS Intel | Install Docker Desktop for Mac (Intel). |
| macOS Apple Silicon | Install Docker Desktop for Mac (Apple Silicon). Then go to **Settings → General** and enable **"Use Rosetta for x86/amd64 emulation"**. |
| Linux | Install Docker Engine + Compose plugin via apt (see README setup section). Then run `sudo usermod -aG docker $USER` and log out/in. |

### VS Code extensions (do this once)

Install these two extensions in VS Code (`Ctrl+Shift+X`):
- **Dev Containers** — by Microsoft (`ms-vscode-remote.remote-containers`)
- **Docker** — by Microsoft (`ms-azuretools.vscode-docker`)

---

## 2. One-time environment setup

### Step 1 — Clone the repo

```bash
git clone git@github.com:TEKS4430/Spring-2026_Task_1.git
cd Spring-2026_Task_1
```

### Step 2 — Create your .env file

```bash
cp .env.example .env
```

Now open `.env` and uncomment the lines for **your OS**:

**Linux:**
```
NETWORK_MODE=host
WEBOTS_HOST=localhost
```

**Mac or Windows:**
```
NETWORK_MODE=bridge
WEBOTS_HOST=host.docker.internal
```

> `.env` is gitignored — it stays on your machine only. Never commit it.

### Step 3 — Open in VS Code

```bash
code .
```

VS Code will show a popup: **"Reopen in Container"** — click it.

> If you miss the popup: `Ctrl+Shift+P` → **Dev Containers: Reopen in Container**

The first build takes **3–5 minutes**. After that it's instant.

When the bottom-left corner of VS Code shows **"Dev Container: ROS2 Jazzy"** you are inside the container. ✅

---

## 3. Workflow


1. Open Webots on your host OS, open the assignment world file (in webots simulator, File -> Open World)
### You should see the text in your Webots terminal as shown in the image marked in red.
![Webots window](https://github.com/TEKS4430/Spring-2026_Task_1/blob/main/screenshots/webots.png)
2. Open VS Code → Reopen in Container (instant after first build)
![VSCode open](https://github.com/TEKS4430/Spring-2026_Task_1/blob/main/screenshots/opening%20vs%20code.png)
![Reopen in container](https://github.com/TEKS4430/Spring-2026_Task_1/blob/main/screenshots/reopen.png)
##### The first time it will take some time to build the container. After building, it will open a terminal inside the container. If you close it or it disappears, simply open a new terminal in VS Code — it will also be inside the container.
3. Edit code in VS Code as normal
4. Open terminal in VS Code (Ctrl+`) — this is inside the container
5. Build and run your ROS2 code from that terminal
6. When done, push your code from a HOST terminal (not container)






## 4. Building and running

All commands below are run **inside the container terminal** (`Ctrl+`` in VS Code).

### Build the workspace

```bash
cb          # alias for: colcon build --symlink-install
src         # alias for: source install/setup.bash
```

Or the full commands:
```bash
cd /ros2_ws
colcon build --symlink-install
source install/setup.bash
```

> `--symlink-install` means Python files are symlinked rather than copied —
> you don't need to rebuild after editing a `.py` file, only after adding new
> nodes or changing `setup.py`.

### Build a single package (faster)

```bash
cbs my_package    # alias for: colcon build --symlink-install --packages-select
```

### Launch the full simulation

```bash
ros2 launch my_package robot.launch.py
```

> Make sure Webots is already open with the correct world before running this.
> You should get a message on the terminal that webots simulator is successfully connected




![build and launch](https://github.com/TEKS4430/Spring-2026_Task_1/blob/main/screenshots/build_launch.png)

### Then in another terminal inside vscode run this commands:
```bash
source install/setup.bash
ros2 topic pub /cmd_vel geometry_msgs/Twist  "linear: { x: 0.1 }"
```
### The robot should be moving in the simulator (Congratulations!)
<!-- ### Run a single node

```bash
ros2 run my_package example_node
``` -->

### Useful debugging commands

```bash
rn                          # alias: ros2 node list
rt                          # alias: ros2 topic list
ros2 topic echo /chatter    # print messages on a topic
ros2 topic hz /cmd_vel      # check publish rate
ros2 node info /example_node
ros2 run rqt_graph rqt_graph   # visual node/topic graph (needs display)
```

---

## 5. Project structure

```
assignmentX/
├── .devcontainer/
│   └── devcontainer.json       # VS Code container config
├── docker/
│   └── Dockerfile              # ROS2 environment definition
├── src/
│   └── my_package/           # ← YOUR CODE LIVES HERE
│       ├── my_package/
│       │   ├── __init__.py
│       │   └── example_node.py # starter node — copy & modify
│       ├── launch/
│       │   └── robot.launch.py # launch file
│       ├── resource/
│       ├── package.xml
│       ├── setup.py            # register new nodes here
│       └── setup.cfg
|       └── worlds                   # Webots .wbt world files
├── docker-compose.yml
├── .env.example                # copy to .env, set your OS values
├── .env                        # gitignored — your local settings
├── .gitignore
└── README.md
```

<!-- ---

## 6. Adding a new node

1. Create `src/my_package/my_package/my_new_node.py`
2. Register it in `setup.py` under `entry_points`:
   ```python
   'my_new_node = my_package.my_new_node:main',
   ```
3. Rebuild:
   ```bash
   cb && src
   ```
4. Run it:
   ```bash
   ros2 run my_package my_new_node
   ```

--- -->


## 7. Troubleshooting

**"Reopen in Container" doesn't appear**
→ Install the **Dev Containers** extension by Microsoft in VS Code.

**Build fails with "package not found"**
→ Run `rosdep install --from-paths src --ignore-src -r -y` inside the container terminal.

**`ros2 launch` can't connect to Webots**
→ Check Webots is open on your host with the correct world loaded.
→ Check your `.env` has the right `WEBOTS_HOST` for your OS.
→ On Linux, verify `NETWORK_MODE=host` is set in `.env`.

**Changes to Python files not reflected after rebuild**
→ Run `src` (re-source the workspace) in your container terminal.
→ If that doesn't work, run `cb` to rebuild.

**Mac Apple Silicon: container build fails**
→ Go to Docker Desktop → Settings → General → enable **"Use Rosetta for x86/amd64 emulation"**.

**"colcon: command not found"**
→ The ROS2 environment isn't sourced. Run:
```bash
source /opt/ros/jazzy/setup.bash
```

---

*ROS2 Jazzy Jalisco · Webots R2025a · Docker*



## Part B: Self-reflection and AI use

In part B, you will reflect on the new skills you have learned and analyze your own work and learning process. You will consider what technical skills you learned while completing part A, what tools you used, why you chose to use them, and what benefits or challenges were associated with their use.

If you did not use AI tools, you should focus on self-reflection regarding your own learning process and discuss your motivations for not using AI as a tool.

The use of AI tools is also allowed in completing part B. However, you should still take responsibility for your own learning and approach the reporting seriously. Ultimately, you are studying for your own benefit.

The use of AI must be reported transparently and appropriately (this is also required by university policies). When completing Sections A and B (note: AI use is generally prohibited in part C), you must keep detailed records of:

- which AI tools you used (e.g., ChatGPT, Copilot, Gemini, Codex, VSCode extensions, etc.),

- the specific language model version (e.g., GPT-5.4),

- and the settings or modes used (e.g., thinking mode, instant mode, or agent mode).

You may also use any other models or technologies, such as locally running language models in your own environment (for example, models run through environments like Ollama) or other AI agent systems.

The primary motivation of this section is to encourage continuous reflection on your learning, both in terms of technical skills and the technologies used to implement solutions.


## Returning instructions

The assignment must be submitted in video format. Create a video that reports Parts A and B, demonstrating that you have successfully set up the environment, explaining how you learned to use your codebase, and presenting your self-reflection as well as describing how you used AI in the assignment.

In the video, use software such as Microsoft Teams to record your screen while presenting and recording your voice. In the recording, you should demonstrate that your environment is running correctly and show the most essential parts of your codebase. In addition, you should use PowerPoint, Google Slides, or a similar tool to document Part B and present it in the video.

This process will not only teach you how to present your work to others, but it will also help facilitate peer learning and support among students. Although in this first assignment there is only a small amount of technical implementation to report, you will learn the submission procedure that will be used for the rest of the assignments, which will be much more implementation-oriented.

We recommend using Microsoft Teams, as it allows you to record both your screen and voice. The recordings are automatically uploaded to SharePoint, which makes it easy to share your recording later for the peer review assignment. Alternatively, you may use other software such as QuickTime Player or OBS to record your video and then upload the recording to SharePoint.

**Important:** You must ensure that your recording is accessible to others who have the link. So, via Sharepoint user interface in your browser (see below) define the shared settings so that anyone who has the link can access the file for maximum number of days. Finally, you should ensure for example in privacy mode or another browser that the link is truly accessible without login.

![create_sharelink](https://github.com/TEKS4430/Spring-2026_Task_1/blob/main/screenshots/accessrights.png)

<img src="[[https://user-images.githubusercontent.com/16319829/81180309-2b51f000-8fee-11ea-8a78-ddfe8c3412a7.png](https://github.com/TEKS4430/Spring-2026_Task_1/blob/main/screenshots/link_settings.png)](https://github.com/TEKS4430/Spring-2026_Task_1/blob/main/screenshots/link_settings.png)" width=50% height=50%>
