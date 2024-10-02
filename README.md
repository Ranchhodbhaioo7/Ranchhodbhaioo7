- 👋 Hi, I’m @soi
- 👀 I’m interested in coding 
- 🌱 I’m currently learning python 
- 💞️ I’m looking to collaborate on YouTube 
- 📫 How to reach me ...

  my car game code
  import pygame
import random

# Initialize pygame
pygame.init()

# Constants
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
CAR_WIDTH = 50
CAR_HEIGHT = 100
OBSTACLE_WIDTH = 50
OBSTACLE_HEIGHT = 100
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
RED = (255, 0, 0)

# Set up display
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Car Game")

# Car class
class Car:
    def __init__(self):
        self.image = pygame.Surface((CAR_WIDTH, CAR_HEIGHT))
        self.image.fill(RED)
        self.rect = self.image.get_rect()
        self.rect.centerx = SCREEN_WIDTH // 2
        self.rect.bottom = SCREEN_HEIGHT - 10
        self.speed = 5

    def move(self, dx):
        self.rect.x += dx * self.speed
        # Keep the car on the screen
        if self.rect.left < 0:
            self.rect.left = 0
        if self.rect.right > SCREEN_WIDTH:
            self.rect.right = SCREEN_WIDTH

    def draw(self, surface):
        surface.blit(self.image, self.rect)

# Obstacle class
class Obstacle:
    def __init__(self):
        self.image = pygame.Surface((OBSTACLE_WIDTH, OBSTACLE_HEIGHT))
        self.image.fill(BLACK)
        self.rect = self.image.get_rect()
        self.rect.x = random.randint(0, SCREEN_WIDTH - OBSTACLE_WIDTH)
        self.rect.y = -OBSTACLE_HEIGHT
        self.speed = 5

    def update(self):
        self.rect.y += self.speed

    def draw(self, surface):
        surface.blit(self.image, self.rect)

# Function to check collision
def check_collision(car, obstacles):
    for obstacle in obstacles:
        if car.rect.colliderect(obstacle.rect):
            return True
    return False

# Main game loop
def game_loop():
    car = Car()
    obstacles = []
    clock = pygame.time.Clock()
    score = 0
    font = pygame.font.Font(None, 36)

    running = True
    while running:
        screen.fill(WHITE)

        # Event handling
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                running = False

        # Car movement
        keys = pygame.key.get_pressed()
        dx = 0
        if keys[pygame.K_LEFT]:
            dx = -1
        if keys[pygame.K_RIGHT]:
            dx = 1
        car.move(dx)

        # Add new obstacles
        if random.randint(1, 30) == 1:
            obstacles.append(Obstacle())

        # Update obstacles
        for obstacle in obstacles:
            obstacle.update()

        # Remove obstacles that are off-screen
        obstacles = [obs for obs in obstacles if obs.rect.y < SCREEN_HEIGHT]

        # Check collision
        if check_collision(car, obstacles):
            running = False  # End the game on collision

        # Draw everything
        car.draw(screen)
        for obstacle in obstacles:
            obstacle.draw(screen)

        # Update score
        score += 1
        score_text = font.render(f"Score: {score}", True, BLACK)
        screen.blit(score_text, (10, 10))

        # Update display
        pygame.display.flip()
        clock.tick(60)

    pygame.quit()

# Start the game
game_loop()
- 😄 visit my channel:@kalilinux--AI
- ⚡ Fun fact: ...

<!---
Ranchhodbhaioo7/Ranchhodbhaioo7 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
