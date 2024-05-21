import pygame
import time
import random

# Initialize Pygame
pygame.init()

# Set up some constants
WIDTH = 800
HEIGHT = 600
CAR_WIDTH = 50
CAR_HEIGHT = 100
FPS = 60

# Set up some colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)

# Set up the car
car_pos = [WIDTH // 2, HEIGHT - CAR_HEIGHT]
car_vel = [0, 0]

# Set up the race track
track_pos = [0, HEIGHT - 100]

# Set up the game clock
clock = pygame.time.Clock()

# Set up the game screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))

# Game loop
running = True
while running:
    # Keep the loop running at the right speed
    clock.tick(FPS)
    
    # Process input (events)
    for event in pygame.event.get():
        # Check for closing the window
        if event.type == pygame.QUIT:
            running = False
        # Check for key presses
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                car_vel[0] = -5
            elif event.key == pygame.K_RIGHT:
                car_vel[0] = 5
        # Check for key releases
        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT and car_vel[0] < 0:
                car_vel[0] = 0
            elif event.key == pygame.K_RIGHT and car_vel[0] > 0:
                car_vel[0] = 0

    # Update the car position
    car_pos[0] += car_vel[0]

    # Check for collision with the track
    if car_pos[0] < track_pos[0] or car_pos[0] + CAR_WIDTH > track_pos[0] + 100:
        car_vel[0] = 0

    # Draw everything
    screen.fill(WHITE)
    pygame.draw.rect(screen, RED, (car_pos[0], car_pos[1], CAR_WIDTH, CAR_HEIGHT))
    pygame.draw.rect(screen, WHITE, (track_pos[0], track_pos[1], 100, 50))

    # After drawing everything, flip the display
    pygame.display.flip()

pygame.quit()
