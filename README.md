# Snake-game
# Here's an example of a simple Snake game implemented in Python using the Pygame library.

  import pygame
import random

# Initialize Pygame
pygame.init()

# Set up the display
width, height = 640, 480
window = pygame.display.set_mode((width, height))
pygame.display.set_caption("Snake Game")

# Define colors
BLACK = (0, 0, 0)
GREEN = (0, 255, 0)
RED = (255, 0, 0)

# Snake initial position and size
snake_size = 20
snake_x = width // 2
snake_y = height // 2

# Snake movement variables
snake_dx = 0
snake_dy = 0

# Initial food position
food_x = round(random.randrange(0, width - snake_size) / 20.0) * 20
food_y = round(random.randrange(0, height - snake_size) / 20.0) * 20

# Clock to control the game's frame rate
clock = pygame.time.Clock()

# Game loop
game_over = False
while not game_over:
    # Handle events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_UP:
                snake_dy = -snake_size
                snake_dx = 0
            elif event.key == pygame.K_DOWN:
                snake_dy = snake_size
                snake_dx = 0
            elif event.key == pygame.K_LEFT:
                snake_dx = -snake_size
                snake_dy = 0
            elif event.key == pygame.K_RIGHT:
                snake_dx = snake_size
                snake_dy = 0

    # Update snake's position
    snake_x += snake_dx
    snake_y += snake_dy

    # Check collision with the boundaries
    if snake_x < 0 or snake_x >= width or snake_y < 0 or snake_y >= height:
        game_over = True

    # Check collision with the food
    if snake_x == food_x and snake_y == food_y:
        # Generate new food
        food_x = round(random.randrange(0, width - snake_size) / 20.0) * 20
        food_y = round(random.randrange(0, height - snake_size) / 20.0) * 20
    else:
        # Remove the last segment of the snake
        pygame.draw.rect(window, BLACK, [snake_x - snake_dx, snake_y - snake_dy, snake_size, snake_size])

    # Draw the snake and the food
    window.fill(BLACK)
    pygame.draw.rect(window, GREEN, [food_x, food_y, snake_size, snake_size])
    pygame.draw.rect(window, RED, [snake_x, snake_y, snake_size, snake_size])

    # Update the display
    pygame.display.update()

    # Set the frame rate
    clock.tick(10)

# Quit Pygame
pygame.quit()
