import pygame,random
pygame.init()
time_clock= pygame.time.Clock()
sc = pygame.display.set_mode((640,480))
pygame.display.set_caption("hungry snake")
bg = pygame.image.load("C:\\mxcmaterials\\贪吃蛇-bg-cde99d04-9f94-4534-82d2-5634e9dbca88.png")


class Snake:
    def __init__(self):
        self.direction="right"
        self.body=[[100,100],[80,100]]
        self.head=self.body[0]
    def draw_me(self):
        for b in self.body:
            pygame.draw.rect(sc,"green",(b[0],b[1],20,20))

    def move_head(self):
        if self.direction == "right":
            self.head[0] +=20
        elif self.direction == "left":
            self.head[0] -=20
        elif self.direction == "up":
            self.head[1] -=20
        elif self.direction == "down":
            self.head[1] +=20
        
    def move_body(self):
        self.body.insert(0,self.head[:])
        self.body.pop()
class Food:
    def __init__(self):
        self.color = "white"
        x = random.randrange(0,640,20)
        y = random.randrange(0,480,20)
        self.position=[x,y]
    def draw_me(self):
        pygame.draw.circle(sc,self.color,(self.position[0]+10,self.position[1]+10),10,0)
    def reset(self):
        self.color = "white"
        x = random.randrange(0,640,20)
        y = random.randrange(0,480,20)
        self.position=[x,y]
snake=Snake()
food=Food()
font = pygame.font.SysFont("Cursive",55,True)
while True:
    sc.blit(bg,(0,0))
    snake.draw_me()
    snake.move_head()
    snake.move_body()
    food.draw_me()
    time_text = font.render("Length: "+str(len(snake.body)),True,(255,0,0))
    sc.blit(time_text,(50,20))
    pygame.display.update()
    time_clock.tick(5)
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            exit()
        elif event.type == pygame.KEYDOWN:
            if event.key== pygame.K_RIGHT:
                if snake.direction !="left":
                     snake.direction ="right"
            if event.key== pygame.K_LEFT:
                if snake.direction !="right":
                     snake.direction ="left"
            if event.key== pygame.K_UP:
                if snake.direction !="down":
                     snake.direction ="up"
            if event.key== pygame.K_DOWN:
                if snake.direction !="up":
                     snake.direction ="down"
    if snake.head==food.position:
        food.reset()
        snake.body.insert(0,snake.head[:])
    if snake.head[0]>620 or snake.head[0]<0 :
        break        
    if snake.head[1]>460 or snake.head[1]<0 :    
        break


time_text = font.render("gameover ",True,(255,0,0))
sc.blit(time_text,(300,200))


pygame.display.update()












input()
