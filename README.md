// variáveis da bolinha
let xBolinha = 200;
let yBolinha = 100;
let diametro = 15;
let raio = diametro / 2;

// variáveis da bolinha
let velocidadeXBolinha = 6;
let velocidadeYBolinha = 6;

let colidiu = false;

// variáveis da raquete oponente
let xRaqueteOponente = 585;
let yRaqueteOponente = 150;
let velocidadeYOponente;

// variáveis da raquete
let xRaquete = 5;
let yRaquete = 150;
let raqueteLargura = 10;
let raqueteAltura = 90;

let meusPontos = 0;
let pontosOponente = 0;

//sons do jogo
  
let ponto;
let trilha;
let raquetada;

function preload(){
  trilha = loadSound("trilha.mp3");
  ponto = loadSound("ponto.mp3");
  raquetada = loadSound("raquetada.mp3");
}
  
function setup() {
  createCanvas(600, 400);
  trilha.loop();
}

function draw() {
  background(169,169,169);
  mostraBolinha();
  mostraRaquete(xRaquete,yRaquete);
  mostraRaquete(xRaqueteOponente,yRaqueteOponente);
  movimentaMinhaRaquete();
  movimentaRaqueteOponente();
  movimentaBolinha();
  verificaColisaoBorda();
  verificaColisaoRaquete(xRaquete,yRaquete);
  verificaColisaoRaquete(xRaqueteOponente,yRaqueteOponente);
  incluiPlacar();
  marcaPonto();
  }

function mostraBolinha(){ 
  fill("#3F51B5")
  circle(xBolinha,yBolinha,diametro); 
  }

function mostraRaquete(){
  fill("#FFC107")
  rect(xRaquete, yRaquete, raqueteLargura, raqueteAltura);
  }

function mostraRaquete(x,y){
  fill("#FFC107")
  rect(x,y,raqueteLargura,raqueteAltura);
  }  

function movimentaMinhaRaquete(){
  if(keyIsDown(UP_ARROW)){
    yRaquete -= 10;
  }

  if(keyIsDown(DOWN_ARROW)){
    yRaquete += 10;
  }
  }

function movimentaRaqueteOponente(){
  if(keyIsDown(87)){
    yRaqueteOponente -= 10;
  }

  if(keyIsDown(83)){
    yRaqueteOponente += 10;
  }
  }

function movimentaBolinha(){
  xBolinha += velocidadeXBolinha;
  yBolinha += velocidadeYBolinha; 
  }

function verificaColisaoBorda(){
  if (xBolinha + raio > width || xBolinha - raio < 0){
    velocidadeXBolinha *= -1;
  }
  
  if (yBolinha + raio > height || yBolinha - raio < 0){
    velocidadeYBolinha *= -1;
  }
  }/*
function verificaColisaoRaquete(){
  if (xBolinha-raio < xRaquete + raqueteLargura
    && yBolinha - raio < yRaquete + raqueteAltura);
  velocidadeXBolinha *= -1;
  }
*/
function verificaColisaoRaquete(x,y){
  colidiu = collideRectCircle(x,y,raqueteLargura,raqueteAltura,xBolinha,yBolinha,raio);
  
  if (colidiu) {

    velocidadeXBolinha *= - 1;
    raquetada.play();
  }
} 

function incluiPlacar(){
  stroke("red");
  textAlign(CENTER);
  textSize(16);
  fill("white");
  
  //placar meusPontos
  fill("orange");
  rect(135,10,35,20);
  fill("black");
  text(meusPontos,150,26);
  
  //placar pontosOponente
  fill("orange");
  rect(430,10,35,20);
  fill("black");
  text(pontosOponente,445,26);
  }

function marcaPonto()  
{  
  if (xBolinha >590){
    meusPontos += 1;
    ponto.play();
  }
  
  if (xBolinha < 10){
    pontosOponente += 1;
    ponto.play();
  }

}
