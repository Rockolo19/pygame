# pygame
# tetris
import pygame
import random

# Initialize Pygame
pygame.init()

# Set the screen size
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))

# Define the colors
black = (0, 0, 0)
white = (255, 255, 255)
red = (255, 0, 0)
green = (0, 255, 0)
blue = (0, 0, 255)
yellow = (255, 255, 0)

# Define the game board
block_size = 30
rows = screen_height // block_size
cols = screen_width // block_size
board = [[black for _ in range(cols)] for _ in range(rows)]

# Define the Tetrominos
tetrominos = [
    [[1, 1, 1, 1]], 
    [[1, 1, 0], [0, 1, 1]],
    [[0, 1, 1], [1, 1, 0]],
    [[1, 1, 1], [0, 1, 0]],
    [[1, 1, 0], [0, 1, 1]],
    [[0, 1, 0], [1, 1, 1]],
    [[1, 0, 0], [1, 1, 1]],
]

# Define the Tetromino colors
tetromino_colors = [
    red,
    green,
    blue,
    yellow,
    white,
    red,
    green,
    blue,
    yellow,
    white,
]

# Define the current Tetromino
current_tetromino = random.choice(tetrominos)
current_color = random.choice(tetromino_colors)
current_row = 0
current_col = cols // 2 - len(current_tetromino[0]) // 2

# Draw the Tetrominos
def draw_tetromino(tetromino, color, row, col):
    for i in range(len(tetromino)):
        for j in range(len(tetromino[0])):
            if tetromino[i][j] == 1:
                pygame.draw.rect(screen, color, (col+j)*block_size, (row+i)*block_size, block_size)

# Main game loop
while True:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                current_col -= 1
            elif event.key == pygame.K_RIGHT:
                current_col += 1
            elif event.key == pygame.K_DOWN:
                current_row += 1

    # Clear the screen
    screen.fill(black)

    # Draw the game board
    for i in range(rows):
        for j in range(cols):
            pygame.draw.rect(screen, board[i][j], (j*block_size, i*block_size, block_size, block_size))

    # Draw the current Tetromino
    draw_tetromino(current_tetromino, current_color, current_row, current_col)

    # Update the screen
    pygame.display.update()
