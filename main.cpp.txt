#include<fstream>
#include<iostream>
#include<math.h>
#include <SFML/Graphics.hpp>
using namespace std;
const float LEN = 40;
const float LEN2 = 15;
float to_radians(int degree)
{
	return degree * 3.14159 / 180.0;
}
bool fd_in_boundary(float cursor_center_x, float cursor_center_y,
	int angle, int distance)
{
	cursor_center_x += distance * cos(to_radians(270 + angle));
	cursor_center_y += distance * sin(to_radians(270 + angle));
	if (cursor_center_x > 0 && cursor_center_x < 500 && cursor_center_y>0 && cursor_center_y < 500)
	{
		return true;
	}
	return false;
}
bool bk_in_boundary(float cursor_center_x, float cursor_center_y,
	int angle, int distance)
{
	cursor_center_x -= distance * cos(to_radians(270 + angle));
	cursor_center_y -= distance * sin(to_radians(270 + angle));
	if (cursor_center_x > 0 && cursor_center_x < 500 && cursor_center_y>0 && cursor_center_y < 500)
	{
		return true;
	}
	return false;
}
sf::RectangleShape fd(float& cursor_center_x, float& cursor_center_y,
	float& cursor_tip_x, float& cursor_tip_y,
	float& cursor_right_hand_x, float& cursor_right_hand_y,
	float& cursor_left_hand_x, float& cursor_left_hand_y, int angle, int distance, sf::Color col, int thickness)
{
	sf::RectangleShape rectangle(sf::Vector2f(distance, thickness));
	rectangle.setPosition(sf::Vector2f(cursor_tip_x, cursor_tip_y));
	rectangle.setFillColor(col);
	rectangle.setOutlineColor(col);
	rectangle.rotate(angle - 90);


	cursor_center_x += distance * cos(to_radians(270 + angle));
	cursor_center_y += distance * sin(to_radians(270 + angle));
	cursor_tip_x = cursor_center_x + LEN2 * cos(to_radians(270 + angle));
	cursor_tip_y = cursor_center_y + LEN2 * sin(to_radians(270 + angle));
	cursor_right_hand_x = cursor_center_x + LEN * cos(to_radians(60 + angle));
	cursor_right_hand_y = cursor_center_y + LEN * sin(to_radians(60 + angle));
	cursor_left_hand_x = cursor_center_x + LEN * cos(to_radians(120 + angle));
	cursor_left_hand_y = cursor_center_y + LEN * sin(to_radians(120 + angle));
	return rectangle;
}




sf::RectangleShape bk(float& cursor_center_x, float& cursor_center_y,
	float& cursor_tip_x, float& cursor_tip_y,
	float& cursor_right_hand_x, float& cursor_right_hand_y,
	float& cursor_left_hand_x, float& cursor_left_hand_y, int angle, int distance, sf::Color col, int thickness)
{
	sf::RectangleShape rectangle(sf::Vector2f(distance, thickness));
	rectangle.setPosition(sf::Vector2f(cursor_tip_x, cursor_tip_y));
	rectangle.setFillColor(col);
	rectangle.setOutlineColor(col);
	rectangle.rotate(angle + 90);

	cursor_center_x -= distance * cos(to_radians(270 + angle));
	cursor_center_y -= distance * sin(to_radians(270 + angle));
	cursor_tip_x = cursor_center_x + LEN2 * cos(to_radians(270 + angle));
	cursor_tip_y = cursor_center_y + LEN2 * sin(to_radians(270 + angle));
	cursor_right_hand_x = cursor_center_x + LEN * cos(to_radians(60 + angle));
	cursor_right_hand_y = cursor_center_y + LEN * sin(to_radians(60 + angle));
	cursor_left_hand_x = cursor_center_x + LEN * cos(to_radians(120 + angle));
	cursor_left_hand_y = cursor_center_y + LEN * sin(to_radians(120 + angle));
	return rectangle;
}
void rt(float& cursor_center_x, float& cursor_center_y,
	float& cursor_tip_x, float& cursor_tip_y,
	float& cursor_right_hand_x, float& cursor_right_hand_y,
	float& cursor_left_hand_x, float& cursor_left_hand_y, int angle)
{
	cursor_tip_x = cursor_center_x + LEN2 * cos(to_radians(270 + angle));
	cursor_tip_y = cursor_center_y + LEN2 * sin(to_radians(270 + angle));
	cursor_right_hand_x = cursor_center_x + LEN * cos(to_radians(60 + angle));
	cursor_right_hand_y = cursor_center_y + LEN * sin(to_radians(60 + angle));
	cursor_left_hand_x = cursor_center_x + LEN * cos(to_radians(120 + angle));
	cursor_left_hand_y = cursor_center_y + LEN * sin(to_radians(120 + angle));
}
void lt(float& cursor_center_x, float& cursor_center_y,
	float& cursor_tip_x, float& cursor_tip_y,
	float& cursor_right_hand_x, float& cursor_right_hand_y,
	float& cursor_left_hand_x, float& cursor_left_hand_y, int angle)
{
	cursor_tip_x = cursor_center_x + LEN2 * cos(to_radians(270 + angle));
	cursor_tip_y = cursor_center_y + LEN2 * sin(to_radians(270 + angle));
	cursor_right_hand_x = cursor_center_x + LEN * cos(to_radians(60 + angle));
	cursor_right_hand_y = cursor_center_y + LEN * sin(to_radians(60 + angle));
	cursor_left_hand_x = cursor_center_x + LEN * cos(to_radians(120 + angle));
	cursor_left_hand_y = cursor_center_y + LEN * sin(to_radians(120 + angle));
}
sf::CircleShape circle(float cursor_tip_x, float cursor_tip_y, int radius, sf::Color col, int thickness)
{
	sf::CircleShape shape(radius);
	shape.setFillColor(sf::Color(0, 0, 0, 0));
	shape.setOutlineColor(col);
	shape.setOutlineThickness(thickness);
	shape.setPosition(cursor_tip_x - radius, cursor_tip_y - radius);
	shape.setFillColor(sf::Color(0, 0, 0, 0));
	return shape;
}
sf::Color pickColor(int num)
{
	int rgbValues[][3] = {
		{255, 0, 0},    // red
		{0, 0, 255},    // blue
		{0, 255, 0},    // green
		{255, 255, 0},  // yellow
		{128, 0, 128},  // purple
		{255, 165, 0},  // orange
		{255, 192, 203}, // pink
		{165, 42, 42},  // brown
		{255, 255, 255}, // white
		{128, 128, 128}  // gray
	};
	return sf::Color(rgbValues[num][0], rgbValues[num][1], rgbValues[num][2]);
}

void penUp(bool& pd)
{
	pd = false;
}
void penDown(bool& pd)
{
	pd = true;
}
void width(int& thickness, int newvalue)
{
	if (newvalue >= 1 && newvalue <= 3)
	{
		thickness = newvalue;
	}
}


void insertCharacter(char arr[], int& currentPosition, int asciiValue) {
	// Check if the array is full
	if (currentPosition >= 100) {
		cout << "Array is already full. Cannot insert more characters.\n";
		return;
	}

	// Check if ASCII value is for backspace
	if (asciiValue == 8) {
		// Move backward by placing a null character
		if (currentPosition > 0) {
			arr[currentPosition - 1] = '\0';
			currentPosition--;
		}
	}
	else if (asciiValue == 13) {  // Check if ASCII value is for Enter
		// Insert null character at the current position
		arr[currentPosition] = '\0';
		// Display the character array
		cout << "Resulting array: " << arr << "\n";
		currentPosition = 0;  // Reset the position to the beginning
	}
	else {
		// Insert the corresponding character at the current position
		arr[currentPosition] = static_cast<char>(asciiValue);
		currentPosition++;
	}
}


bool isSubstringAtPosition(const char* mainStr, const char* subStr, int& position) {
	// Check if position is valid
	int startpos = position;
	while (mainStr[position] == ' ')
	{
		position++;
	}
	if (position < 0 || position + strlen(subStr) > strlen(mainStr)) {
		return false;
	}

	// Iterate through the characters in subStr
	for (int i = 0; subStr[i] != '\0'; ++i) {
		// Convert characters to lowercase for case-insensitive comparison
		char mainChar = tolower(mainStr[position]);
		position++;
		char subChar = tolower(subStr[i]);

		// Compare characters
		if (mainChar != subChar) {
			position = startpos;
			return false;
		}
	}

	// All characters matched, subStr is present at the specified position
	return true;
}
int convertDigitsToInt(const char* input, int& position) {
	int result = 0;
	bool digitFound = false;

	// Skip spaces before the first digit
	while (std::isspace(input[position])) {
		position++;
	}

	// Check if a digit is present
	if (!std::isdigit(input[position])) {
		return -1; // No digit found
	}

	// Convert consecutive digits to int
	while (std::isdigit(input[position])) {
		digitFound = true;
		result = result * 10 + (input[position] - '0');
		position++;
	}

	// Update the character and index after the numbers
	position = position;

	return digitFound ? result : -1; // Return the result or -1 if no digit was found
}



int findColorIndex(const char* input, int& position) {
	// Define the colors in small alphabets
	const char* colors[] = { "red", "blue", "green", "yellow", "purple", "orange", "pink", "brown", "white", "gray" };

	// Skip initial spaces
	while (std::isspace(static_cast<unsigned char>(input[position]))) {
		++position;
	}

	// Iterate over each color
	for (int i = 0; i < 10; ++i) {
		// Calculate the length of the color
		size_t colorLength = std::strlen(colors[i]);

		// Perform a case-insensitive check for the substring
		bool match = true;
		for (size_t j = 0; j < colorLength; ++j) {
			if (std::tolower(static_cast<unsigned char>(input[position + j])) !=
				std::tolower(static_cast<unsigned char>(colors[i][j]))) {
				match = false;
				break;
			}
		}

		if (match) {
			position += strlen(colors[i]);
			return i;  // Return the index of the matching color
		}
	}

	// No match found
	return -1;
}

void copySubstringTo2DArray(char dest[][101], const char source[], int destRow, int startIndex, int endIndex) {
	// Ensure valid indices
	if (destRow < 0 || destRow >= 39 || startIndex < 0 || endIndex >= 100 || startIndex > endIndex) {
		std::cerr << "Invalid indices or parameters." << std::endl;
		return;
	}

	// Ensure destination row has enough space
	size_t substringLength = endIndex - startIndex + 1;

	if (strlen(source) < static_cast<size_t>(endIndex + 1 - startIndex)) {
		std::cerr << "Not enough characters in the source array." << std::endl;
		return;
	}

	// Copy the substring from source to the destination row in dest using strncpy_s
	strncpy_s(dest[destRow], sizeof(dest[destRow]), source + startIndex, substringLength);
	dest[destRow][substringLength] = '\0';
}
void addCommand(char commands[100][101], char newCommand[101]) {
	// Shift existing commands up by one row
	for (int i = 100 - 1; i > 0; --i) {
		strcpy_s(commands[i], 101, commands[i - 1]);
	}

	// Copy the new command to the first row
	strcpy_s(commands[0], 101, newCommand);
}
void save(char commandHistory[100][101], string fileName)
{
	// Open the file for writing
	std::ofstream outFile(fileName);

	// Check if the file is opened successfully
	if (!outFile.is_open()) {
		std::cerr << "Error opening file: " << fileName << std::endl;
		return;
	}

	// Iterate through rows of commandHistory
	for (int i = 0; i < 100; ++i) {
		// Check for a null row
		if (commandHistory[i][0] == '\0') {
			// Stop writing when a null row is encountered
			break;
		}

		// Write the row as a line in the file
		outFile << commandHistory[i] << '\n';
	}

	// Close the file
	outFile.close();
}
int load(char commandHistory[100][101], string fileName) {
	// Open the file for reading
	std::ifstream inFile(fileName);

	// Check if the file is opened successfully
	if (!inFile.is_open()) {
		std::cerr << "Error opening file: " << fileName << std::endl;
		return 0; // Return 0 to indicate no lines loaded
	}

	int linesLoaded = 0;

	// Iterate through rows of commandHistory
	for (int i = 0; i < 100; ++i) {
		// Read a line from the file
		inFile.getline(commandHistory[i], 101);

		// Stop reading when the end of the file is reached or a null row is encountered
		if (!inFile || commandHistory[i][0] == '\0') {
			break;
		}

		linesLoaded++;
	}

	// Close the file
	inFile.close();

	return linesLoaded;
}

int main()
{
	string filename="";
	char commandHistory[100][101] = {0};
	sf::Color col = sf::Color::Red;
	int angle = 0;
	int thickness = 1;
	char command[101] = { 0 };
	int currentPosition = 0;
	bool pd = true;// true means pendown so can draw, if false means pen up, will not draw.

	sf::RenderWindow window(sf::VideoMode(700, 530), "SFML works!");
	int circlenum = 0;
	int linenum = 0;
	sf::CircleShape shape, circlesarray[100];
	sf::RectangleShape linearray[100];
	shape.setFillColor(sf::Color(0, 0, 0, 0));
	shape.setOutlineColor(col);
	cout << shape.getOutlineThickness();
	shape.setOutlineThickness(1);
	shape.setPosition(0.f, 125.0f);
	shape.setFillColor(sf::Color(0, 0, 0, 128));
	bool focus = true;
	bool first = true;
	float cursor_center_x = 125.0f, cursor_center_y = 125.0f;
	float cursor_tip_x = cursor_center_x + LEN2 * cos(to_radians(270)),
		cursor_tip_y = cursor_center_y + LEN2 * sin(to_radians(270)),
		cursor_right_hand_x = cursor_center_x + LEN * cos(to_radians(60)),
		cursor_right_hand_y = cursor_center_y + LEN * sin(to_radians(60)),
		cursor_left_hand_x = cursor_center_x + LEN * cos(to_radians(120)),
		cursor_left_hand_y = cursor_center_y + LEN * sin(to_radians(120));


	sf::Vertex line[2];
	line[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
	line[0].color = col;
	line[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);
	line[1].color = col;


	sf::Vertex line2[2];
	line2[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
	line2[0].color = col;
	line2[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);
	line2[1].color = col;

	sf::Vertex line3[2];
	line3[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
	line3[0].color = col;
	line3[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);
	line3[1].color = col;


	sf::Vertex line4[2];
	line4[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
	line4[0].color = col;
	line4[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);
	line4[1].color = col;


	sf::Vertex boundary[2];
	boundary[0].position = sf::Vector2f(0, 500);
	boundary[0].color = col;
	boundary[1].position = sf::Vector2f(700, 500);
	boundary[1].color = col;



	sf::Vertex boundary2[2];
	boundary2[0].position = sf::Vector2f(500, 0);
	boundary2[0].color = col;
	boundary2[1].position = sf::Vector2f(500, 500);
	boundary2[1].color = col;


	shape = circle(cursor_tip_x, cursor_tip_y, 45, col, thickness);





	sf::Font font;
	if (!font.loadFromFile("arial.ttf"))
	{
		// error...
	}



	sf::Text text;

	// select the font
	text.setFont(font); // font is a sf::Font

	// set the string to display
	text.setString("");

	// set the character size
	text.setCharacterSize(19); // in pixels, not points!
	text.setPosition(0, 500);

	// set the color
	text.setFillColor(sf::Color::Red);






	sf::Text htext[16];

	for (int i = 0;i < 16;i++)
	{
		// select the font
		htext[i].setFont(font); // font is a sf::Font

		// set the string to display
		htext[i].setString("abc");

		// set the character size
		htext[i].setCharacterSize(19); // in pixels, not points!
		htext[i].setPosition(500, i*30);

		// set the color
		htext[i].setFillColor(sf::Color::Red);
	}
	
	int pos;
	while (window.isOpen())
	{
		sf::Event event;
		while (window.pollEvent(event))
		{
			if (event.type == sf::Event::Closed)
				window.close();
			else if (event.type == sf::Event::GainedFocus)
			{
				cout << "Gained" << endl;
				focus = true;
			}
			else if (event.type == sf::Event::LostFocus)
			{
				cout << "Lost" << endl;
				focus = false;
			}
			else if (event.type == sf::Event::TextEntered)
			{
				int ascii = event.text.unicode;
				if (ascii >= 65 && ascii <= 90)
				{
					ascii += 32;
				}
				//cout << ascii;
				insertCharacter(command, currentPosition, ascii);
				text.setString(command);
				if (ascii == 13)
				{
					pos = 0;
					bool read_command = true;
					bool read_repeat_commands = false;
					int repeatCount = 0;
					char repeat_command[39][101] = { 0 };
					int repeat_command_count = 0;
					bool error = false;
					int repeat_command_exec = 0;
					bool execute_load = false;
					int loadcount = 0;
					while (read_command || read_repeat_commands || repeatCount!=0||(execute_load&&loadcount!=0))
					{
						if (execute_load)
						{
							pos = 0;
							loadcount--;
							memcpy(command, commandHistory[loadcount], 101);
						}
						if (!read_command && !read_repeat_commands&&!execute_load)
						{
							
							if (repeatCount!=0&&repeat_command_exec == repeat_command_count * repeatCount)
							{
								cout << "\nrepeatcomplete\n";
								break;
							}
							for (int i = 0;i < circlenum;i++)
							{
								window.draw(circlesarray[i]);
							}
							for (int i = 0;i < linenum;i++)
							{
								window.draw(linearray[i]);
							}
							//window.draw(rect);
							window.draw(text);
							first = false;
							window.display();
							//system("pause");
							cout << "\nCOPYING\n"<<repeatCount<<endl<<repeat_command_count<<endl<<repeat_command_exec<<endl;
							memcpy(command, repeat_command[repeat_command_exec % repeat_command_count], 101);
							cout << endl << command << endl;
							pos = 0;
							repeat_command_exec++;
						}
						if (repeat_command_exec==0&&repeat_command_count > 0)
						{
							if (command[pos] != ' ' && command[pos] != ']')
							{
								error = true;
								cout << endl << "1err" << endl;
								break;
							}
						}
						int start = pos, end = -1;
						if (!read_repeat_commands && isSubstringAtPosition(command, "repeat", pos))
						{
							cout << "repeat\n";
							int temp = convertDigitsToInt(command, pos);
							if (temp < 0)
							{
								error = true;

								cout << endl << "2err" << endl;
								break;
							}
							cout << temp << endl;
							repeatCount = temp;
							cout << repeatCount << endl;
							cout << endl << command[pos] << endl;
							if (isSubstringAtPosition(command, "[", pos))
							{
								cout << "INSHAALLAH";
								read_repeat_commands = true;
							}
							else
							{
								error = true;

								cout << endl << "3err" << endl;
								break;
							}
							start = pos;
						}
						else if (read_repeat_commands && isSubstringAtPosition(command, "]", pos))
						{
							if (command[pos] == 0)
							{
								cout << "REPEAT COMMANDS READ";
								read_repeat_commands = false;
								addCommand(commandHistory, command);

							}
							else {
								error = true;

								cout << endl << "4err" << endl;
								break;
							}
						}
						else if (isSubstringAtPosition(command, "fd", pos))
						{
							cout << "forward\n";
							int temp = convertDigitsToInt(command, pos);
							if (temp < 0)
							{
								error = true;

								cout << endl << "5err" << endl;
								break;
							}
							cout << endl << command[pos] << endl;
							cout << temp << endl;
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									if (fd_in_boundary(cursor_center_x, cursor_center_y, angle, temp))
									{
										sf::RectangleShape rec = fd(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle, temp, col, thickness);
										if (pd)
										{
											linearray[linenum] = rec;
											linenum++;
										}
										line[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line2[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line2[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);

										line3[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line3[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line4[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line4[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);
									}
								}
								else
								{
									error = true;
									break;
								}


							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "forward", pos))
						{
							cout << "forward\n";
							int temp = convertDigitsToInt(command, pos);
							cout << temp << endl;
							if (temp < 0)
							{
								error = true;

								cout << endl << "6err" << endl;
								break;
							}
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									if (fd_in_boundary(cursor_center_x, cursor_center_y, angle, temp))
									{
										sf::RectangleShape rec = fd(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle, temp, col, thickness);
										if (pd)
										{
											linearray[linenum] = rec;
											linenum++;
										}
										line[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line2[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line2[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);

										line3[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line3[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line4[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line4[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);

									}
								}
								else
								{
									error = true;
									break;
								}

							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "bk", pos))
						{
							cout << "back\n";
							int temp = convertDigitsToInt(command, pos);
							cout << temp << endl;
							if (temp < 0)
							{
								error = true;

								cout << endl << "7err" << endl;
								break;
							}
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									if (bk_in_boundary(cursor_center_x, cursor_center_y, angle, temp))
									{
										sf::RectangleShape rec = bk(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle, temp, col, thickness);
										if (pd)
										{
											linearray[linenum] = rec;
											linenum++;
										}
										line[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line2[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line2[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);

										line3[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line3[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line4[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line4[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);
									}
								}
								else
								{
									error = true;
									break;
								}
							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "rt", pos))
						{
							cout << "right\n";
							int temp = convertDigitsToInt(command, pos);
							cout << temp << endl;
							if (temp < 0 && !(temp % 30 == 0 || temp % 45 == 0))
							{
								error = true;

								cout << endl << "8err" << endl;
								break;
							}
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									if (temp % 30 == 0 || temp % 45 == 0)
									{
										fd(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle, LEN2, col, thickness);
										angle = angle + temp;
										
										rt(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle);
										bk(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle, LEN2, col, thickness);
										line[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line2[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line2[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);

										line3[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line3[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line4[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line4[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);

									}
								}
								else
								{
									error = true;
									break;
								}

							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "lt", pos))
						{
							cout << "left\n";
							int temp = convertDigitsToInt(command, pos);
							cout << temp << endl;
							if (temp < 0 && !(temp % 30 == 0 || temp % 45 == 0))
							{
								error = true;

								cout << endl << "9err" << endl;
								break;
							}
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									cout << "temp" << temp << endl;
									if (temp % 30 == 0 || temp % 45 == 0)
									{
										fd(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle, LEN2, col, thickness);
										angle = angle - temp;
										lt(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle);
										bk(cursor_center_x, cursor_center_y,
											cursor_tip_x, cursor_tip_y,
											cursor_right_hand_x, cursor_right_hand_y,
											cursor_left_hand_x, cursor_left_hand_y, angle, LEN2, col, thickness);

										cout << "\nleftleft\n";


										line[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line2[0].position = sf::Vector2f(cursor_tip_x, cursor_tip_y);
										line2[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);

										line3[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line3[1].position = sf::Vector2f(cursor_right_hand_x, cursor_right_hand_y);

										line4[0].position = sf::Vector2f(cursor_center_x, cursor_center_y);
										line4[1].position = sf::Vector2f(cursor_left_hand_x, cursor_left_hand_y);
									}
								}
								else {
									error = true;
									break;
								}
							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "pu", pos))
						{
							cout << "penup\n";
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									penUp(pd);
								}
								else
								{
									error = true;

									cout << endl << "10err" << endl;
									break;
								}
							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "pd", pos))
						{
							cout << "pendown\n";
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									penDown(pd);
								}
								else
								{
									error = true;

									cout << endl << "11err" << endl;
									break;
								}
							}

							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "color", pos))
						{
							cout << "color\n";
							if (command[pos] == ' ')
							{
								int c = findColorIndex(command, pos);
								if (c != -1)
								{
									if (!read_repeat_commands)
									{
										if (command[pos] == 0)
										{
											if (!read_repeat_commands && command[pos] == 0)
											{
												col = pickColor(c);
												line[0].color = col;
												line2[0].color = col;
												line3[0].color = col;
												line4[0].color = col;
												line[1].color = col;
												line2[1].color = col;
												line3[1].color = col;
												line4[1].color = col;
											}
										}
										else
										{
											error = true;
											break;
										}
									}
								}
								else
								{
									error = true;

									cout << endl << "12err" << endl;
									break;
								}
							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "width", pos))
						{
							cout << "width\n";
							int temp = convertDigitsToInt(command, pos);
							cout << temp << endl;
							if (temp == -1)
							{
								error = true;

								cout << endl << "13err" << endl;
								break;
							}
							if (command[pos] == 0)
							{
								if (!read_repeat_commands)
								{
									width(thickness, temp);
								}
								else
								{
									error = true;

									cout << endl << "14err" << endl;
									break;
								}
							}

							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "circle", pos))
						{
							cout << "circle\n";
							int temp = convertDigitsToInt(command, pos);
							cout << temp << endl;
							if (temp == -1)
							{
								error = true;

								cout << endl << "15err" << endl;
								break;
							}
							if (!read_repeat_commands && pd)
							{
								if (command[pos] == 0 && temp >= 0 && temp < 125)
								{
									circlesarray[circlenum] = circle(cursor_tip_x, cursor_tip_y, temp, col, thickness);
									circlenum++;
								}
								else
								{
									error = true;

									cout << endl << "16err" << endl;
									break;
								}
							}
							end = pos - 1;
						}
						else if (isSubstringAtPosition(command, "cs", pos))
						{
							cout << "clear screen\n";
							if (!read_repeat_commands)
							{
								if (command[pos] == 0)
								{
									circlenum = 0;
									linenum = 0;
								}
								else
								{
									error = true;

									cout << endl << "17err" << endl;
									break;
								}
							}
							end = pos - 1;
						}
						else if (!read_repeat_commands && isSubstringAtPosition(command, "save", pos))
						{
							cout << "save\n";
							if (command[pos] == ' ')
							{
								while (command[pos] == ' ')
								{
									pos++;
								}
								int substringLength = strlen(command + pos);
								// Create a string variable and copy the substring into it
								filename=string(command + pos, substringLength);

								// Print the extracted string
								std::cout << "Extracted String: " << filename << std::endl;
								if (filename == "")
								{
									error = true;
									break;
								}
								else
								{
									save(commandHistory, filename);
								}
							}
						}
						else if (!read_repeat_commands && isSubstringAtPosition(command, "load", pos))
						{
							cout << "load\n";
							if (command[pos] == ' ')
							{
								while (command[pos] == ' ')
								{
									pos++;
								}
								int substringLength = strlen(command + pos);
								// Create a string variable and copy the substring into it
								filename=string(command + pos, substringLength);

								// Print the extracted string
								std::cout << "Extracted String: " << filename << std::endl;
								if (filename == "")
								{
									error = true;
									break;
								}
								else
								{
									loadcount=load(commandHistory, filename);
									if (loadcount)
									{
										execute_load = true;
									}
								}
							}
						}
						if (!read_command && read_repeat_commands)
						{
							cout << "Start\t" << start << endl;
							cout << "End\t" << end << endl;
							//system("pause");
							copySubstringTo2DArray(repeat_command, command, repeat_command_count, start, end);
							puts(repeat_command[repeat_command_count]);
							repeat_command_count++;
						}
						//start = pos - 1;
						read_command = false;
					}
					if (error)
					{
						cout << "ERROR\n";

					}
					else
					{
						if (!execute_load && repeat_command_exec == 0 && repeatCount == 0)
						{
							addCommand(commandHistory, command);
						}
					}
					for (int i = 0; i < 101; ++i) {
						command[i] = '\0';
					}
					cout<< commandHistory[0][0] <<(commandHistory[0][1])<<commandHistory[0][2];
					//system("pause");
					text.setString(command);
				}
			}
		}
		window.clear();
		window.draw(line, 2, sf::Lines);
		window.draw(line2, 2, sf::Lines);
		window.draw(line3, 2, sf::Lines);
		window.draw(line4, 2, sf::Lines);
		window.draw(boundary, 2, sf::Lines);
		window.draw(boundary2, 2, sf::Lines);
		for (int i = 0;i < circlenum;i++)
		{
			window.draw(circlesarray[i]);
		}
		for (int i = 0;i < linenum;i++)
		{
			window.draw(linearray[i]);
		}
		for (int i = 0;i < 16;i++)
		{
			htext[i].setString(commandHistory[i]);
			window.draw(htext[i]);
		}
		//window.draw(rect);
		window.draw(text);
		first = false;
		window.display();
		//if (first)
		{

		}
	}

	return 0;
}