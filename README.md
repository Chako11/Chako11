import pygame

import random

# Initialize Pygame

pygame.init()

# Set up the display

display_width = 800

display_height = 600

game_display = pygame.display.set_mode((display_width, display_height))

pygame.display.set_caption("My Game")

# Colors

black = (0, 0, 0)

white = (255, 255, 255)

# Player

player_width = 50

player_height = 50

player_x = display_width // 2 - player_width // 2

player_y = display_height - player_height - 10

# Obstacle

obstacle_width = 100

obstacle_height = 100

obstacle_x = random.randrange(0, display_width - obstacle_width)

obstacle_y = -obstacle_height

obstacle_speed = 5

clock = pygame.time.Clock()

game_over = False

# Game Loop

while not game_over:

    for event in pygame.event.get():

        if event.type == pygame.QUIT:

            game_over = True

    keys = pygame.key.get_pressed()

    if keys[pygame.K_LEFT] and player_x > 0:

        player_x -= 5

    if keys[pygame.K_RIGHT] and player_x < display_width - player_width:

        player_x += 5

    game_display.fill(white)

    pygame.draw.rect(game_display, black, [player_x, player_y, player_width, player_height])

    pygame.draw.rect(game_display, black, [obstacle_x, obstacle_y, obstacle_width, obstacle_height])

    obstacle_y += obstacle_speed

    if obstacle_y > display_height:

        obstacle_y = -obstacle_height

        obstacle_x = random.randrange(0, display_width - obstacle_width)

    if player_y < obstacle_y + obstacle_height:

        if player_x < obstacle_x + obstacle_width and player_x + player_width > obstacle_x:

            game_over = True

    pygame.display.update()

    clock.tick(60)

# Quit the game

pygame.quit()



