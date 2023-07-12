import pygame

# Definición de colores
NEGRO = (0, 0, 0)
BLANCO = (255, 255, 255)
AZUL = (0, 0, 255)
VERDE = (0, 255, 0)
ROJO = (255, 0, 0)
VIOLETA = (255, 0, 255)

class Pared(pygame.sprite.Sprite):
    """Esta clase representa la barra inferior que controla al protagonista"""

    def __init__(self, x, y, largo, alto, color):
        """Función Constructor"""
        super().__init__()

        self.image = pygame.Surface([largo, alto])
        self.image.fill(color)

        self.rect = self.image.get_rect()
        self.rect.y = y
        self.rect.x = x

class Protagonista(pygame.sprite.Sprite):
    """Esta clase representa al protagonista"""

    cambio_x = 0
    cambio_y = 0

    def __init__(self, x, y):
        """Función Constructor"""
        super().__init__()

        self.image = pygame.Surface([15, 15])
        self.image.fill(BLANCO)

        self.rect = self.image.get_rect()
        self.rect.y = y
        self.rect.x = x

    def cambiovelocidad(self, x, y):
        """Cambia la velocidad del protagonista"""
        self.cambio_x += x
        self.cambio_y += y

    def mover(self, paredes):
        """Encuentra una nueva posición para el protagonista"""

        self.rect.x += self.cambio_x

        lista_impactos_bloques = pygame.sprite.spritecollide(self, paredes, False)
        for bloque in lista_impactos_bloques:
            if self.cambio_x > 0:
                self.rect.right = bloque.rect.left
            else:
                self.rect.left = bloque.rect.right

        self.rect.y += self.cambio_y

        lista_impactos_bloques = pygame.sprite.spritecollide(self, paredes, False)
        for bloque in lista_impactos_bloques:
            if self.cambio_y > 0:
                self.rect.bottom = bloque.rect.top
            else:
                self.rect.top = bloque.rect.bottom

class Cuarto:
    """Clase base para todos los cuartos"""

    def __init__(self):
        """Constructor, crea nuestras listas"""
        self.pared_lista = pygame.sprite.Group()
        self.sprites_enemigos = pygame.sprite.Group()

class Cuarto1(Cuarto):
    """Crea todas las paredes del cuarto 1"""

    def __init__(self):
        super().__init__()

        # Crear las paredes. (x_pos, y_pos, largo, alto, color)
        paredes = [
            [0, 0, 20, 250, BLANCO],
            [0, 350, 20, 250, BLANCO],
            [780, 0, 20, 250, BLANCO],
            [780, 350, 20, 250, BLANCO],
            [20, 0, 760, 20, BLANCO],
            [20, 580, 760, 20, BLANCO],
            [390, 50, 20, 500, AZUL]
        ]

        for item in paredes:
            pared = Pared(item[0], item[1], item[2], item[3], item[4])
            self.pared_lista.add(pared)

class Cuarto2(Cuarto):
    """Crea todas las paredes del cuarto 2"""

    def __init__(self):
        super().__init__()

        paredes = [
            [0, 0, 20, 250, ROJO],
            [0, 350, 20, 250, ROJO],
            [780, 0, 20, 250, ROJO],
            [780, 350, 20, 250, ROJO],
            [20, 0, 760, 20, ROJO],
            [20, 580, 760, 20, ROJO],
            [190, 50, 20, 500, VERDE],
            [590, 50, 20, 500, VERDE]
        ]

        for item in paredes:
            pared = Pared(item[0], item[1], item[2], item[3], item[4])
            self.pared_lista.add(pared)

class Cuarto3(Cuarto):
    """Crea todas las paredes del cuarto 3"""

    def __init__(self):
        super().__init__()

        paredes = [
            [0, 0, 20, 250, VIOLETA],
            [0, 350, 20, 250, VIOLETA],
            [780, 0, 20, 250, VIOLETA],
            [780, 350, 20, 250, VIOLETA],
            [20, 0, 760, 20, VIOLETA],
            [20, 580, 760, 20, VIOLETA]
        ]

        for item in paredes:
            pared = Pared(item[0], item[1], item[2], item[3], item[4])
            self.pared_lista.add(pared)

        for x in range(100, 800, 100):
            for y in range(50, 451, 300):
                pared = Pared(x, y, 20, 200, ROJO)
                self.pared_lista.add(pared)

        for x in range(150, 700, 100):
            pared = Pared(x, 200, 20, 200, BLANCO)
            self.pared_lista.add(pared)

def main():
    """Programa Principal"""

    pygame.init()
    pantalla = pygame.display.set_mode([800, 600])
    pygame.display.set_caption('Maze Runner')

    protagonista = Protagonista(50, 50)
    desplazarsprites = pygame.sprite.Group()
    desplazarsprites.add(protagonista)

    cuartos = [Cuarto1(), Cuarto2(), Cuarto3()]
    cuarto_actual_no = 0
    cuarto_actual = cuartos[cuarto_actual_no]

    reloj = pygame.time.Clock()
    hecho = False
    puntuacion = 0

    while not hecho:
        for evento in pygame.event.get():
            if evento.type == pygame.QUIT:
                hecho = True

            if evento.type == pygame.KEYDOWN:
                if evento.key == pygame.K_LEFT:
                    protagonista.cambiovelocidad(-5, 0)
                if evento.key == pygame.K_RIGHT:
                    protagonista.cambiovelocidad(5, 0)
                if evento.key == pygame.K_UP:
                    protagonista.cambiovelocidad(0, -5)
                if evento.key == pygame.K_DOWN:
                    protagonista.cambiovelocidad(0, 5)

            if evento.type == pygame.KEYUP:
                if evento.key == pygame.K_LEFT:
                    protagonista.cambiovelocidad(5, 0)
                if evento.key == pygame.K_RIGHT:
                    protagonista.cambiovelocidad(-5, 0)
                if evento.key == pygame.K_UP:
                    protagonista.cambiovelocidad(0, 5)
                if evento.key == pygame.K_DOWN:
                    protagonista.cambiovelocidad(0, -5)

        protagonista.mover(cuarto_actual.pared_lista)

        if protagonista.rect.x < -15:
            cuarto_actual_no = (cuarto_actual_no - 1) % len(cuartos)
            cuarto_actual = cuartos[cuarto_actual_no]
            protagonista.rect.x = 790
            puntuacion += 10
        if protagonista.rect.x > 801:
            cuarto_actual_no = (cuarto_actual_no + 1) % len(cuartos)
            cuarto_actual = cuartos[cuarto_actual_no]
            protagonista.rect.x = 0
            puntuacion += 10

        pantalla.fill(NEGRO)
        desplazarsprites.draw(pantalla)
        cuarto_actual.pared_lista.draw(pantalla)

        # Dibujar puntuación en la pantalla
        fuente = pygame.font.Font(None, 36)
        texto_puntuacion = fuente.render("Puntuación: " + str(puntuacion), True, BLANCO)
        pantalla.blit(texto_puntuacion, (20, 30))

        pygame.display.flip()

        reloj.tick(60)

    pygame.quit()

if __name__ == "__main__":
    main()

