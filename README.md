#include <stdio.h>
#include <stdlib.h>
#include "/usr/include/SDL/SDL.h"
#include "/usr/include/SDL/SDL_image.h"
#include "/usr/include/SDL/SDL_mixer.h"
#include "/usr/include/SDL/SDL_events.h"
#include "/usr/include/SDL/SDL_mouse.h"

typedef struct{
    SDL_Surface *image;
    SDL_Rect pos;
}simple;

void main(){
    simple screen,image,character,minimap,icon;
    SDL_Event event;
    screen.image = SDL_SetVideoMode(1000, 500, 32, SDL_HWSURFACE | SDL_DOUBLEBUF);
    image.image = IMG_Load("map.png");
    character.image = IMG_Load("character.png");
    minimap.image = IMG_Load("maptest.png");
    icon.image = IMG_Load("icontest.png");


    image.pos.x = 0;
    image.pos.y = 0; 


    screen.pos.x = 0;
    screen.pos.y = 0;
    screen.pos.w = image.image->w;
    screen.pos.h = image.image->h;


    character.pos.x = 23;
    character.pos.y = 275; 

    minimap.pos.x = 799;
    minimap.pos.y = 0; 

    icon.pos.x = 804;
    icon.pos.y = 55;


    //start
    
    while(1){
        SDL_BlitSurface(image.image,NULL,screen.image,&image.pos);
        SDL_BlitSurface(character.image,NULL,screen.image,&character.pos);
        SDL_BlitSurface(minimap.image,NULL,screen.image,&minimap.pos);
        SDL_BlitSurface(icon.image,NULL,screen.image,&icon.pos);
        SDL_Flip(screen.image);
        while(SDL_PollEvent(&event)){
            switch(event.type){
                case SDL_QUIT:
                    SDL_Quit();
                break;
                case SDL_KEYDOWN:
                    switch(event.key.keysym.sym){
                        case SDLK_RIGHT:
                            if(character.pos.x < 950){
                                character.pos.x += 10;
                                icon.pos.x += 2;
                            }
                        break;
                        case SDLK_LEFT:
                            if(character.pos.x > 10){
                                character.pos.x -= 10;
                                icon.pos.x -= 2;
                            }
                        break;
                    }
                break;
                }
            }
    }
    SDL_FreeSurface(screen.image);
}
