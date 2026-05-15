var _direita_wasd = keyboard_check(ord("D"));
var _esquerda_wasd = keyboard_check(ord("A"));
var _cima_wasd = keyboard_check(ord("W"));
var _baixo_wasd = keyboard_check(ord("S"));

var _direita_seta = keyboard_check(vk_right);
var _esquerda_seta = keyboard_check(vk_left);
var _cima_seta = keyboard_check(vk_up);
var _baixo_seta = keyboard_check(vk_down);

var _direita = _direita_wasd || _direita_seta;
var _esquerda = _esquerda_wasd || _esquerda_seta;
var _cima = _cima_wasd || _cima_seta;
var _baixo = _baixo_wasd || _baixo_seta;

var _parado = !(_direita || _esquerda || _cima || _baixo);

// Movimentação com verificação precisa de colisões
if (_direita) {
    if (!place_meeting(x + vel, y, obj_colisor)) {
        x += vel;
    } else {
        // Ajusta movimento incremental para evitar travamento
        while (!place_meeting(x + 1, y, obj_colisor)) {
            x += 1;
        }
    }
    sprite_index = Spr_player_movendo_direita;
    ultima_direcao = "direita";
}

if (_esquerda) {
    if (!place_meeting(x - vel, y, obj_colisor)) {
        x -= vel;
    } else {
        while (!place_meeting(x - 1, y, obj_colisor)) {
            x -= 1;
        }
    }
    sprite_index = Spr_player_movendo_esquerda;
    ultima_direcao = "esquerda";
}

if (_cima) {
    if (!place_meeting(x, y - vel, obj_colisor)) {
        y -= vel;
    } else {
        while (!place_meeting(x, y - 1, obj_colisor)) {
            y -= 1;
        }
    }
    sprite_index = Spr_player_movendo_cima;
    ultima_direcao = "cima";
}

if (_baixo) {
    if (!place_meeting(x, y + vel, obj_colisor)) {
        y += vel;
    } else {
        while (!place_meeting(x, y + 1, obj_colisor)) {
            y += 1;
        }
    }
    sprite_index = Spr_player_movendo_baixo;
    ultima_direcao = "baixo";
}

// Quando o jogador parar, usa a sprite da última direção
if (_parado) {
    switch (ultima_direcao) {
        case "direita":
            sprite_index = Spr_player_parado_direita;
            break;
        case "esquerda":
            sprite_index = Spr_player_parado_esquerda;
            break;
        case "cima":
            sprite_index = Spr_player_parado_cima;
            break;
        case "baixo":
            sprite_index = Spr_player_parado_baixo;
            break;
    }
}
