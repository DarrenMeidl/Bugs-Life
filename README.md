# 🐞 Bug's Life

A C++ simulation of bugs crawling, hopping, and flying around a 10x10 board, built with SFML. Bugs fight and eat each other whenever they land on the same cell, and the simulation runs until only one bug is left standing. You can also jump in as the SuperBug and control it yourself with the arrow keys.

> **Note:** The original commit history for this project is on the `master` branch, not `main`.

## 📦 Technologies

- `C++`
- `SFML`
- `CMake`
- `CLion`

## ⚙️ Features

Here's what you can do in Bug's Life:

- **Load the Bug Board**: Load all the bugs from a text file and place them on the board. Each line in the file describes the type of bug, its ID, its starting position, direction, size, and hop length where it applies.

- **Bug Types**: There are three types of bugs, plus a player. Crawlers move one cell at a time. Hoppers hop several cells in a straight line. Flyers hop several cells diagonally. If any of them hit the edge of the board, they stop or pick a new direction.

- **Display and Find Bugs**: Print every bug on the board, or search for a single bug by its ID.

- **Tap the Board**: Every bug moves once, then any bugs sharing a cell fight. The biggest bug wins and eats the others, absorbing their size up to a maximum of 20. If there's a tie for biggest, the winner is picked at random.

- **Life History**: See the path every bug has taken and whether it's still alive or who ate it.

- **Display All Cells**: List every cell on the board along with the bugs inside it.

- **Run the Simulation**: The board is tapped automatically every second and drawn in an SFML window with a sprite for each bug. Sprites scale with the size of the bug. The simulation ends when there is only one bug left.

- **Play as the SuperBug**: During the simulation, use the arrow keys to move the SuperBug around the board and try to eat everything else.

- **Save to File**: Exiting writes the life history of every bug to a file with the date and time. The simulation also keeps a live copy of the life history in its own file.

## 🔨 The Process

I started with the `Bug` base class, which holds everything bugs have in common like an ID, a position, a direction, a size, and a path of everywhere they've been. From there I built the `Crawler` and `Hopper` classes, each with their own way of moving.

Next, I created the `Board` and `Cell` classes. The board reads the bugs from the text file, creates the right type of bug for each line, and stores them all as `Bug` pointers in a vector. Each cell keeps a list of the bugs currently sitting on it. With that in place, I added the menu options to display bugs, find a bug by ID, tap the board, and show the life history.

After that, I added the fight and eat feature. After every move, each cell with two or more bugs finds the biggest one, picks a random winner if there's a tie, and marks the rest as eaten.

Then I added the `Flyer`, which moves diagonally instead of in straight lines, and the simulation option that taps the board every second until one bug remains.

Finally, I brought in SFML to draw the board and the bugs in a window. I also added the `SuperBug`, which is controlled by the player with the arrow keys instead of moving randomly. To finish, I made sure all the memory allocated for the bugs and cells is freed when the program ends.

## 📚 What I Learned

During this project, I got a much better understanding of object-oriented programming in C++ and how to manage memory by hand.

### 🧬 Inheritance and Polymorphism:

- **Base Classes**: I used a `Bug` base class with child classes that override `move()` and `printBug()`. Storing everything as `Bug*` pointers meant I could treat every bug the same way and let each type decide how it behaves.

### 🧠 Memory Management:

- **Pointers**: Since all the bugs and cells are created with `new`, I had to make sure everything gets deleted when the program ends. This taught me to keep track of where memory is allocated and freed.

### 📄 Reading and Writing Files:

- **Parsing Data**: I used `ifstream` and `stringstream` to read each line of the bug file and split it on the semicolons. I also used `ofstream` to write the life histories out with a timestamp.

### 🎲 Random Numbers:

- **Random Movement**: I used `mt19937` to give bugs random directions and to break ties in fights.

### 🧭 Coordinates and Boundaries:

- **Board Edges**: Working out when a bug is blocked by the edge of the board, especially for the Flyer moving diagonally, took careful thinking. The board's y values also go downwards as negative numbers, so I had to keep flipping signs to find the right cell.

### 🖼️ Discovering SFML:

- **Graphics and Input**: I learned how to open a window, draw the board with rectangles, draw bug sprites scaled to their size, and handle keyboard events for the SuperBug.

### 📈 Overall Growth:

Each part of this project helped me understand more about structuring a larger C++ program across multiple classes, managing memory, and connecting a simulation to a graphical window. It was more than just making bugs move around. It was about breaking a big problem into smaller classes that each do one job.

## ✔️ How can it be improved?

- Load each bug texture once instead of loading the image from disk every time a bug is drawn.
- Use smart pointers instead of `new` and `delete` to manage memory.
- Use the board's width and height instead of hard-coding the edges of the board.
- Add a win or game over message in the window when the SuperBug wins or gets eaten.
- Let the user choose the board size and the bug file.
- Add more bug types with their own movement patterns.

## 🚚 Running the Project

To run the project in your local environment, follow these steps:

1. Clone the repository to your local machine.
2. Install SFML 2.6.1 to `C:/SFML-2.6.1`, or update the `SFML_DIR` and `include_directories` paths in `CMakeLists.txt` to wherever you installed it.
3. Open the project in CLion (or any CMake-compatible IDE) and build it.
4. Run the program from the build folder, such as `cmake-build-debug`. The code looks for `../bugs.txt` and `../Bug Images/`, so it needs to be run one folder down from the project root.
5. In the console menu, enter `1` first to load the bugs, then `7` to run the simulation. Use the arrow keys to move the SuperBug.
6. Enter `8` to exit and save the life history of all the bugs to a file.

## 📽️ Video

*Link unavailable at this time.*
