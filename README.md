# AIRFORCE-
import pygame

# 1.2 - Initialize the game 
pygame.init()
width, height = 640, 480
screen = pygame.display.set_mode((width, height))
keep_going = True

# 1.3 - Load images
player = pygame.image.load("airforce pygame/pictures/Drawing.sketchpad (3).png")
cargo = pygame.image.load("airforce pygame/pictures/Drawing-1.sketchpad.png")
background = pygame.image.load("airforce pygame/pictures/bg.jpg")
background = pygame.transform.scale(background, (width, height))

# Initialize player position
player_pos = [130, 100]

# 1.4 - Use loop to keep the game running 
while keep_going:
    # 1.5 - Clear the screen before drawing it again
    screen.fill(0)

    # 1.6 - Draw the screen elements
    screen.blit(background, (0, 0))
    screen.blit(player, player_pos)
    screen.blit(cargo, (0, 30))
    screen.blit(cargo, (0, 135))
    screen.blit(cargo, (0, 240))
    screen.blit(cargo, (0, 345))

    # 1.7 - Update the screen
    pygame.display.flip()  # will update the contents of the entire display, and faster than .update()

    # 1.8 - Loop through the events
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            keep_going = False

    # Handle key states for movement
    keys = pygame.key.get_pressed()
    key_up = keys[pygame.K_w]
    key_down = keys[pygame.K_s]
    key_left = keys[pygame.K_a]
    key_right = keys[pygame.K_d]

    # Update player position based on key presses
    if key_up:
        player_pos[1] -= 5  # Move up
    if key_down:
        player_pos[1] += 5  # Move down
    if key_left:
        player_pos[0] -= 5  # Move left
    if key_right:
        player_pos[0] += 5  # Move right
    if key_up:
      player_pos[1]-=1
    elif key_down:
      player_pos[1]+=1
    if key_left:
      player_pos[0]-=1
    elif key_right:
      player_pos[0]+=1
    if key_up and player_pos[1]>0:
        player_pos[1]-=1
    elif key_down and player_pos[1]<height-30:
        player_pos[1]+=1
    if key_left and player_pos[0]>0:
        player_pos[0]-=1
    elif key_right and player_pos[0]<width-100:
        player_pos[0]+=1

    # Optional: Prevent the player from moving off screen
    player_pos[0] = max(0, min(width - player.get_width(), player_pos[0]))
    player_pos[1] = max(0, min(height - player.get_height(), player_pos[1]))

    #bullets
    bullets=[]
    bullet = pygame.image.load("Drawing-2.sketchpad.png")
    if event.type==pygame.MOUSEBUTTONDOWN or (event.type==pygame.KEYDOWN and event.key==pygame.K_SPACE):
        bullets.append([player_pos[0],player_pos[1]]) 
    for bulletPos in bullets:

        bulletPos[0]=bulletPos[0]+1
        screen.blit(bullet,bulletPos)
        if bulletPos[0]<-64 or bulletPos[0]>640 or bulletPos[1]<-64 or bulletPos[1]>480:
        bullets.pop(index)  #remove from list
        index+=1  
# 1.9 Exit pygame and python
pygame.quit()
exit(0)

