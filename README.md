# pygame
# tetris
    import pygame
    import random

    pygame.init()

    screen_width = 800
    screen_height = 600
    screen = pygame.display.set_mode((screen_width, screen_height))

    black = (0, 0, 0)
    white = (255, 255, 255)
    red = (255, 0, 0)
    green = (0, 255, 0)
    blue = (0, 0, 255)
    yellow = (255, 255, 0)

    block_size = 30
    rows = screen_height // block_size
    cols = screen_width // block_size
    board = [[black for _ in range(cols)] for _ in range(rows)]
    
    tetrominos = [
        [[1, 1, 1, 1]], 
        [[1, 1, 0], [0, 1, 1]],
        [[0, 1, 1], [1, 1, 0]],
        [[1, 1, 1], [0, 1, 0]],
        [[1, 1, 0], [0, 1, 1]],
        [[0, 1, 0], [1, 1, 1]],
        [[1, 0, 0], [1, 1, 1]],
    ]
    
    
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
    
    current_tetromino = random.choice(tetrominos)
    current_color = random.choice(tetromino_colors)
    current_row = 0
    current_col = cols // 2 - len(current_tetromino[0]) // 2
    
    def draw_tetromino(tetromino, color, row, col):
        for i in range(len(tetromino)):
            for j in range(len(tetromino[0])):
                if tetromino[i][j] == 1:
                    pygame.draw.rect(screen, color, (col+j)*block_size, (row+i)*block_size, block_size)

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

    screen.fill(black)

    for i in range(rows):
        for j in range(cols):
            pygame.draw.rect(screen, board[i][j], (j*block_size, i*block_size, block_size, block_size))

    draw_tetromino(current_tetromino, current_color, current_row, current_col)

    pygame.display.update()
