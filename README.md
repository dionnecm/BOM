# BOM - Biblioteca de Objetos Matemáticos

O arquivo selaReta.scad foi desenvolvido no programa OpenSCAD versão 2021.01.
Este arquivo constrói todas as lâminas para compor uma sela através de retas. Os sólidos que compõem todas as peças foram formados através de diversos cubos. Para imprimir toda a sela são necessários mais de 200 mil partes e o OpenSCAD não consegue executar a renderização para este número de peças.
É recomendável imprimir cada peça separada. Para isso os laços for(x=[-50:10:50]) e for(y=[-50:10:50]) devem indicar qual a peça deverá ser impressa. Cada eixo é composto por 11 peças e que no laço variam de [-50,+50] com passo de 10, que é a separação entre as peças. Para imprimir a peça 40 no eixo x deve-se colocar o laço em for(x=[40:10:40]), ou seja, os limites inferior e superior do laço devem ser iguais e devem pertencer ao conjunto {-50, -40, -30, -20, -10, 0, 10 , 20, 30, 40, 50}

## Exemplo: Para imprimir a peça 40 o seguinte cógio deverá ser utilizado:
```
largura = 5;
profundidade = 5;
ponto_focal = 90;
numero_laminas = 50;
altura = 90;
sulco = 25;    // Altura dos sulcos

module lamina_sela_y_45(y, largura, profundidade) {
    for (x = [-(numero_laminas+largura):0.1:numero_laminas+largura]){
        translate([x, y, 0])
        cube([largura, profundidade, -2*x*y/ponto_focal + altura], center = false);
    }
}


// As lâminas variam de -[50, +50] com passo de 10.
// Para imprimir uma lâmina colocar o loop em y=[30:10:30]
for(y=[-40:10:40]) {
    translate([0,0,0]) rotate([0,0,0]) {
        difference() {
            lamina_sela_y_45(y, largura, profundidade);
            for(x=[-50:10:50]) {
                translate ([x+2.5, 0, 0])
                cube([largura+1, 120, sulco * 2], center = true);
            }
        }    
    }
}


module lamina_sela_x_45(x, largura, profundidade) {
    for (y = [-(numero_laminas+largura):0.1:numero_laminas+largura]){
        translate([x, y, 0])
        cube([largura, profundidade, -2*x*y/ponto_focal + altura], center = false);
    }
}


// As lâminas variam de -[50, +50] com passo de 10.
// Para imprimir uma lâmina colocar o loop em x=[30:10:30]
for(x=[40:10:40]) {
    translate([0,0,0]) rotate([0,90,0]) {
        difference() {
            lamina_sela_x_45(x, largura, profundidade);
            for(y=[-50:10:50]) {
                translate ([0, y+2.5, 89.5])
                cube([122, largura+1, sulco * 5], center = true);
            }
        }    
    }
}
```
## Equipe de desenvolvimento
- Márcio Nascimento
- Dionne Monteiro
- Felipe Neves
