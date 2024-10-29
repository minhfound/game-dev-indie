import pygame, sys, math

fps= 60
width =1400
height =900
bsize= 64
screen=pygame.display.set_mode((width,height),pygame.RESIZABLE)

map_test = [
['x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','h','h','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','h','h','h','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','h','h','h','h','h','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','h','h','h','h','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','h','h','.','t','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','t','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','t','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','t','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],
['x','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','.','x'],    
['x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x','x'],
]

class Game:
    def __init__(self):
        pygame.init()
        pygame.display.set_caption('fixed')
        self.clock = pygame.time.Clock()

    def run(self):
        while True:    
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    pygame.quit()
                    sys.exit()
            
            player.update()
            enemy.update(player)
            screen.fill((0, 0, 0))
            player.draw(screen)
            enemy.draw(screen)
            pygame.display.update()
            self.clock.tick(fps)

class Bullet():
    def __init__(self, x, y, direct):
        self.image = pygame.Surface((10, 10))
        self.image.fill((255, 255, 0))  
        self.rect = self.image.get_rect(center=(x, y))
        self.speed = 10
        self.direct = direct

    def update(self):
        self.rect.x += self.direct[0] * self.speed
        self.rect.y += self.direct[1] * self.speed

    def draw(self, win):
        win.blit(self.image, self.rect)
        

class Player():
    def __init__(self, x, y):
        self.image = pygame.Surface((50, 50))
        self.image.fill((0, 255, 0))
        self.rect = self.image.get_rect(center=(x, y))
        self.bullets = []
        self.direct = (0, -1)  

    def update(self):
        keys = pygame.key.get_pressed()
        if keys[pygame.K_a]:
            self.rect.x -= 5
            self.direct = (-1, 0) 
            if keys[pygame.K_q]:
              self.rect.x -=15 
        if keys[pygame.K_d]:
            self.rect.x += 5
            self.direct = (1, 0)
            if keys[pygame.K_q]:
              self.rect.x +=15
        if keys[pygame.K_w]:
            self.rect.y -= 5
            self.direct = (0, -1) 
            if keys[pygame.K_q]:
              self.rect.y -=15
        if keys[pygame.K_s]:
            self.rect.y += 5
            self.direct = (0, 1) 
            if keys[pygame.K_q]:
              self.rect.y +=15

        if keys[pygame.K_SPACE]:  
            bullet = Bullet(self.rect.centerx, self.rect.centery, self.direct)
            self.bullets.append(bullet)

        for bullet in self.bullets[:]:
            bullet.update()
            if bullet.rect.x < 0 or bullet.rect.x > width or bullet.rect.y < 0 or bullet.rect.y > height:
                self.bullets.remove(bullet) 

    def draw(self, win):
        win.blit(self.image, self.rect)
        for bullet in self.bullets:
            bullet.draw(win)

class Enemy():
    def __init__(self, x, y):
        self.image = pygame.Surface((50, 50))
        self.image.fill((255, 0, 0))
        self.rect = self.image.get_rect(center=(x, y))
        self.notice_radius=400
    def update(self, player):
        dx, dy = player.rect.x - self.rect.x, player.rect.y - self.rect.y
        dist = math.hypot(dx, dy)
        if dist <=self.notice_radius:
         dx, dy = dx / dist, dy / dist
         self.rect.x += dx * 2
         self.rect.y += dy * 2
    def draw(self, winScreen):
        screen.blit(self.image, self.rect)

x = 50
y = 50
player = Player(500, 500)
enemy = Enemy(100, 100)

game= Game()
game.run()
