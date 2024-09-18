# Down The Marianas Trench Initial Release

# @author Dan Nguyen
# @date 2021/01/28

## Pygame setup
import pygame
import random
pygame.init()
pygame.mixer.init()
size = (1000, 1000)
screen = pygame.display.set_mode(size)
pygame.display.set_caption("Down The Marianas Trench")

## MODEL - Data use in system
# Define various events
scoreEvent = pygame.USEREVENT + 0
enemySpawnEvent = pygame.USEREVENT + 1
spawnIncreased = pygame.USEREVENT + 2
foodSpawnEvent = pygame.USEREVENT + 3
bubbleSpawnEvent = pygame.USEREVENT + 4

# Assign variables for light blue rgb
screenColour = 250
screenColourRed = 50

# Define colours
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
GREEN = (0, 255, 0)
RED = (255, 0, 0)
BLUE = (0, 0, 255)
YELLOW = (255,255,0)

# Player class
class Player():
    def __init__(self):

        # Player attributes
        self.health = 100

        # Player score
        self.score = 0
        self.highScore = 0
        self.time = 1

        # Draw attributes
        self.xSpeed = 0
        self.ySpeed = 0
        self.xPos = 400
        self.yPos = 400

    # Draw the player method
    def draw(self):
        screen.blit(playerImage, playerImagePos)
    
    # Move the player method
    def move(self):
        
        # Updating the position
        self.xPos += self.xSpeed
        self.yPos += self.ySpeed
    
    # Check to see if player hits screen border
    def checkScreenCollision(self):
        
        # Boundary x-axis checking for player
        if self.xPos + 179 > size[0]:
            self.xPos = size[0] - 179
        elif self.xPos - 50 < 0:
            self.xPos = 50
    
    # Basic scoring system calculation
    def scoring(self):
        self.score += self.time

    # Display current score to user
    def displayScore(self):
        pygame.draw.rect(screen, WHITE, [730, 10, 220, 50])
        
        # Convert score integer to string and display to user
        scoreMessage = font.render("Score:" + str(self.score), True, BLACK)
        screen.blit(scoreMessage, [730, 10])

    # Check to see if enemy hits player
    def checkCollision(self,otherObject,tolerance):
        result = False
        
        # Assign x and y values
        x = self.xPos
        y = self.yPos
        
        # Assign another class instance values
        otherX = otherObject.pos[0]
        otherY = otherObject.pos[1]
        
        # x coordinate and y coordinate value less than tolerance
        if (abs(otherX - x) < tolerance and abs(otherY - y) < tolerance):
            
            # Set result to true
            result = True
        
        return result

    # Check to see if food hits player
    def checkFoodCollision(self,otherObject,tolerance):
        collisionResult = False
        
        # Assign x and y values
        x = self.xPos
        y = self.yPos
        
        # Assign another class instance values
        otherX = otherObject.pos[0]
        otherY = otherObject.pos[1]
        
        # x coordinate and y coordinate value less than tolerance
        if (abs(otherX - x) < tolerance and abs(otherY - y) < tolerance):
            
            # Set collision result to true
            collisionResult = True
        
        return collisionResult
    
    # Reset attribute values
    def resetGame(self):
        self.xPos = 400
        self.yPos = 400
        self.xSpeed = 0
        self.score = 0
        self.health = 100
    
    # Display high score to user
    def displayHighScore(self):

        # Add scores to list
        scoresList.append(self.score)

        # Set highest score in list
        self.highScore = max(scoresList)
        
        # Convert high score integer to string and display to user
        pygame.draw.rect(screen, WHITE, [230, 10, 325, 50])
        scoreMessage = font.render("High Score:" + str(self.highScore), True, BLACK)
        screen.blit(scoreMessage, [230, 10])
    
    # Displaying healthbar to user
    def displayHealth(self):
        pygame.draw.rect(screen, WHITE, [100, 900, 345, 50])
        healthColour = GREEN

        # Display healthbar text to user
        healthMessage1 = font.render("HP", True, BLACK)
        screen.blit(healthMessage1, [100, 900])

        # Assign seperate variables for health value
        p = self.health
        l = self.health

        # Health colour is red when low
        if l <= 20:
            healthColour = RED

        # Displaying a 10 x 1 rectangle
        for i in range(1):
            for o in range(10):
                
                # Health is positive
                if p > 0:
                    
                    # Draw row of rectangles
                    pygame.draw.rect(screen, healthColour, [170 + 27 * o, 913 + 27 * i, 25, 25])
                    
                    # Each rectangle represents 10 points
                    p -= 10

# Enemy class
class Enemy():
    def __init__(self):

        # Enemy attributes
        self.health = random.randint(1,50)

        # Draw attributes
        self.speed = [random.randint(1,6), random.randint(1,6)]
        self.pos = [0, 0]
        self.startPos = 1050

    # Draw the enemy method
    def draw(self):
        
        # Assign values
        x = self.pos[0]
        y = self.pos[1]

        screen.blit(enemyImage, [x,y])
    
    # Move the enemy method
    def move(self):

        # Moving horizontally
        self.pos[0] += self.speed[0]
        
        # Moving vertically
        self.pos[1] -= self.speed[1]
        
        # Bounce horizontally from wall to wall
        if (self.pos[0] >= screen.get_width() - 125):
            self.speed[0] = self.speed[0] * -1
            self.pos[0] = screen.get_width() - 125
        elif (self.pos[0] <= 50):
            self.speed[0] = self.speed[0] * -1
            self.pos[0] = 50

# Food class
class Food():
    def __init__(self):

        # Food attributes
        self.health = 10

        # Draw attributes
        self.speed = [random.randint(1,6), random.randint(1,6)]
        self.pos = [0, 0]
        self.startPos = 1050

    # Draw the food method
    def draw(self):
        
        # Assign values
        x = self.pos[0]
        y = self.pos[1]

        screen.blit(foodImage, [x,y])

    # Move the food method
    def move(self):

        # Moving horizontally
        self.pos[0] += self.speed[0]

        # Moving vertically
        self.pos[1] -= self.speed[1]
        
        # Bounce horizontally from wall to wall
        if (self.pos[0] >= screen.get_width() - 175):
            self.speed[0] = self.speed[0] * -1
            self.pos[0] = screen.get_width() - 175
        elif (self.pos[0] <= 50):
            self.speed[0] = self.speed[0] * -1
            self.pos[0] = 50

# Bubble class
class Bubble():
    def __init__(self):

        # Bubble attributes
        self.health = 10

        # Draw attributes
        self.speed = [random.randint(1,6), random.randint(1,6)]
        self.pos = [0, 0]
        self.startPos = 1050

    # Draw the bubble method
    def draw(self):
        
        # Assign values
        x = self.pos[0]
        y = self.pos[1]

        pygame.draw.circle(screen, WHITE, [x, y], 15, 2)

    # Move the bubble method
    def move(self):

        # Moving horizontally
        self.pos[0] += self.speed[0]
        
        # Moving vertically
        self.pos[1] -= self.speed[1]

# Draw screen border lines
def drawBorder(screen,x,y):
    pygame.draw.rect(screen, RED, [0, 0, 50, 1000])
    pygame.draw.rect(screen, RED, [950, 0, 50, 1000])
    for i in range(25):
        pygame.draw.rect(screen, YELLOW, [17.5, 20 + (i * 50), 15, 15])
    for i in range(25):
        pygame.draw.rect(screen, YELLOW, [967.5, 20 + (i * 50), 15, 15])

# Displaying initial start screen to player
def displayInitialInstructions():
    screen.fill(WHITE)

    # Display title message to player
    message1 = font.render("~DOWN THE MARIANAS TRENCH~", True, BLACK)
    screen.blit(message1, [193, 200])

    # Displaying instructions to player
    message2 = smallFont.render("Survive for as long as possible.", False, BLACK)
    screen.blit(message2, [227, 400])
    message2 = smallFont.render("Use arrow keys and mouse to kill and dodge the jellyfish.", False, BLACK)
    screen.blit(message2, [227, 450])
    message2 = smallFont.render("Remember to pick up food to restore your health!!!", False, BLACK)
    screen.blit(message2, [227, 500])
    message3 = font.render("Please press N to begin...", True, BLACK)
    screen.blit(message3, [227, 750])

    # Begin creating various events every specified milliseconds
    pygame.time.set_timer(scoreEvent, 1000)
    pygame.time.set_timer(enemySpawnEvent, 4000)
    pygame.time.set_timer(foodSpawnEvent, 8000)
    pygame.time.set_timer(bubbleSpawnEvent, 1000)

# Displaying game over screen to player
def displayGameOverScreen():
    screen.fill(BLACK)

    # Display game over message to player
    gameOverMessage = font.render("GAMEOVER", True, WHITE)
    screen.blit(gameOverMessage, [390, 445])
    gameOverMessage2 = font.render("Please press N to restart...", True, WHITE)
    screen.blit(gameOverMessage2, [227, 600])

    # Display current score and overall high score
    player.displayScore()
    player.displayHighScore()

# Check mouse click collision box
def checkMouseClick(pos):

    # For every enemy in list
    for enemy in enemyList:

        # Draw enemy collision box
        enemyBox = pygame.Rect(enemy.pos[0], enemy.pos[1], 74, 113)

        # Mouse click position is in collision box
        if enemyBox.collidepoint(pos): 

            # Damage enemy by 25hp
            enemy.health -= 25
            
            # Play enemy hit sound
            enemyHitSound.play()
    
    # For every food in list
    for food in foodList:

        # Draw food collision box
        foodBox = pygame.Rect(food.pos[0], food.pos[1] , 124.9, 74)

        # Mouse click position is in collision box
        if foodBox.collidepoint(pos): 

            # Destroy food
            food.health = 0

            # Add 20 player HP if not full
            if player.health < 100:
                player.health += 20
            
            # Play food hit sound
            foodHitSound.play()

# Increase in difficulty message
def difficultyIncreaseMessage():
    gameOverMessage = font.render("Difficulty Increased!", True, WHITE)
    screen.blit(gameOverMessage, [310, 445])

# Create objects
player = Player()
enemy = Enemy()
food = Food()
bubble = Bubble()

# Importing sea turtle image and assigning position
playerImage = pygame.image.load(r"./Graphics/sea_turtle.png").convert()
playerImage.set_colorkey(BLACK)
playerImagePos = [player.xPos, player.yPos]

# Importing enemy image
enemyImage = pygame.image.load(r"./Graphics/jellyfish.png").convert()
enemyImage.set_colorkey(BLACK)

# Importing food image
foodImage = pygame.image.load(r"./Graphics/food.png").convert()
foodImage.set_colorkey(BLACK)

# Import custom font
font = pygame.font.Font(r"./Assets/somethingfishy.ttf", 50)
smallFont = pygame.font.Font(r"./Assets/somethingfishy.ttf", 25)

# Import user interactive sounds
enemyHitSound = pygame.mixer.Sound(r"./Sounds/enemyhitsound.ogg")
playerDeathSound = pygame.mixer.Sound(r"./Sounds/playerdeathsound.ogg")
playerHitSound = pygame.mixer.Sound(r"./Sounds/playerhitsound.ogg")
foodHitSound = pygame.mixer.Sound(r"./Sounds/foodhit.ogg")

# Set default player speed
speed = 13

# Set default scene to initial
scene = 0

# Game is not over and increased difficulty is off
gameOver = False
difficultyMessage = False

# Create empty list of enemies and scores
enemyList = []
scoresList = []
foodList = []
bubbleList = []

# Loop until user clicks close button
done = False

# Manage screen update rate
clock = pygame.time.Clock()

# Main program loop
while not done:
    ## CONTROL
    # Main event loop
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            done = True

        # Event type is score event and game is not over
        if event.type == scoreEvent and gameOver == False:

            # Adding score per time
            player.scoring()

            # Background colour becoming darker
            if screenColour > 0:
                screenColour -= 5
            if screenColourRed > 0:
                screenColourRed -= 5

            # Score is 30 increase difficulty
            if player.score == 30:

                # Begin creating spawn increased event every second
                pygame.time.set_timer(spawnIncreased, 1000)
                
                # Display difficulty message
                difficultyMessage = True

            # Destroy difficulty message
            elif player.score > 32:
                difficultyMessage = False
        
        # Event type is enemy spawn event or spawn increased and game is not over
        if event.type == enemySpawnEvent or event.type == spawnIncreased and gameOver == False:

            # Create enemy
            oneEnemy = Enemy()
            
            # Set enemy position generate random x coordinate
            oneEnemy.pos = [random.randrange(100, 850), oneEnemy.startPos]
            
            # Add to list
            enemyList.append(oneEnemy)

        # Event type is food spawn event and game is not over
        if event.type == foodSpawnEvent and gameOver == False:

            # Create food
            oneFood = Food()
            
            # Set food position generate random x coordinate
            oneFood.pos = [random.randrange(100, 850), oneFood.startPos]
            
            # Add to list
            foodList.append(oneFood)

        # Event type is bubble spawn event and game is not over
        if event.type == bubbleSpawnEvent and gameOver == False:

            # Create bubble
            oneBubble = Bubble()
            
            # Set bubble position generate random x coordinate
            oneBubble.pos = [random.randrange(100, 850), oneBubble.startPos]
            
            # Add to list
            bubbleList.append(oneBubble)

        # User pressed down a key
        elif event.type == pygame.KEYDOWN:
            
            # Determine if it was an arrow key and adjust speed
            if event.key == pygame.K_LEFT:
                player.xSpeed = -speed
            elif event.key == pygame.K_RIGHT:
                player.xSpeed = speed
            
            # Player presses n to change scene
            elif event.key == pygame.K_n:
                
                # Only change scene if initial
                if scene == 0:
                    scene += 1
                
                # Change scene to initial when gameover
                if scene == 2:
                    scene = 1
                    gameOver = False
                    
                    # Create one spawn increased event and stop
                    pygame.time.set_timer(spawnIncreased, 1000, True)

                    # Call method to reset attributes
                    player.resetGame()

                    # Reassign light blue rgb values
                    screenColour = 250
                    screenColourRed = 50

        # User let up on a key and game is not over
        elif event.type == pygame.KEYUP and gameOver == False:
            
            # If it is an arrow key reset vector back to zero
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                player.xSpeed = 0
        
        # Once mouse is pressed
        elif event.type == pygame.MOUSEBUTTONDOWN:
            
            # Call to check mouse click
            checkMouseClick(event.pos)

    # Game logic

    # Updating player position/coordinates
    playerImagePos = [player.xPos, player.yPos]
    player.move()

    # Check player screen collision
    player.checkScreenCollision()

    # For every object in list move
    for enemy in enemyList:
        enemy.move()
    for food in foodList:
        food.move()
    for bubble in bubbleList:
        bubble.move()

    # Enemy collision with player checking
    for enemy in enemyList:
        if player.checkCollision(enemy, 125):
            
            # Play hit sound
            playerHitSound.play()

            # Damage player health by 20
            player.health -= 20
            enemy.health = 0

        # Player health is 0 gameover
        if player.health <= 0:
            gameOver = True
            scene = 2
            
            # Player death sound
            playerDeathSound.play()

    # Food collision with player checking
    for food in foodList:
        if player.checkFoodCollision(food, 125):
            
            # Play hit sound and remove food
            foodHitSound.play()
            food.health = 0

            # Heal player by 20 if not full
            if player.health < 100:
                player.health += 20

    ## VIEW
    # Assigning variables to light blue rgb value
    LIGHT_BLUE = (screenColourRed, screenColour, screenColour)

    # Clear screen to light blue
    screen.fill(LIGHT_BLUE)

    # Game is not over
    if gameOver == False:
        
        # For every bubble in list draw
        for bubble in bubbleList:
            bubble.draw()

            # Bubble offscreen set health 0
            if bubble.pos[1] <= -50:
                bubble.health = 0
            
            # Bubble health is 0 remove from list
            if bubble.health <= 0:
                bubbleList.remove(bubble)
    
    # Game is over remove any enemies
    else:
        for bubble in bubbleList:
            bubbleList.remove(bubble)

    # Calling to display static elements and user interface
    drawBorder(screen,0,0)
    player.displayScore()
    player.displayHighScore()
    player.displayHealth()
    
    # Draw the player
    player.draw()

    # Game is not over
    if gameOver == False:
        
        # For every enemy in list draw
        for enemy in enemyList:
            enemy.draw()

            # Enemy offscreen set health 0
            if enemy.pos[1] <= -50:
                enemy.health = 0
            
            # Enemy health is 0 remove from list
            if enemy.health <= 0:
                enemyList.remove(enemy)
    
    # Game is over remove any enemies
    else:
        for enemy in enemyList:
            enemyList.remove(enemy)

    # Game is not over
    if gameOver == False:
        
        # For every food in list draw
        for food in foodList:
            food.draw()

            # Food offscreen set health 0
            if food.pos[1] <= -50:
                food.health = 0
            
            # Food health is 0 remove from list
            if food.health <= 0:
                foodList.remove(food)
    
    # Game is over remove any enemies
    else:
        for food in foodList:
            foodList.remove(food)

    # Display difficulty message
    if difficultyMessage == True:
        difficultyIncreaseMessage()

    # Display initial instructions and gameover screen
    if scene == 0:
        displayInitialInstructions()
    elif scene == 2:
        displayGameOverScreen()

    # Update screen
    pygame.display.flip()
 
    # Limit to 60 frames per second
    clock.tick(60)

# Close the window and quit
pygame.quit()
