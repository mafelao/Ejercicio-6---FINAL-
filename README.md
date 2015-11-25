# Ejercicio-6---FINAL-
Visualización interactiva de datos 2D.

Table tabla;  
PImage mapabase;
PImage Colombia;
PFont titles;
PFont numbers;
int rectX, rectY;      // Position of square button
int circleX, circleY;  // Position of circle button
int rectSize = 90;     // Diameter of rect
float datapais;
boolean rectOver = false;
boolean circleOver = false;

int yearSelected = -1;

String anios[]= {"2003", "2004", "2005", "2006", "2007", "2008", "2009", "2010", "2011", "2012"};

void setup() {

  size (1000, 636);
  tabla = loadTable("Tabla1.csv", "header");
  Colombia=loadImage("Colombia.png");
  titles=loadFont("Helvetica-15.vlw");
  numbers=loadFont("Helvetica-12.vlw");
  mapabase=loadImage("mapa1.png");

  textFont(titles, 18);
}

void loadInNewBackgroundImage(String pais) {

  if (pais.equals("Colombia")) {
    mapabase=loadImage("Colombia.png");
  } else if (pais.equals("Argentina")) {
    mapabase=loadImage("Argentina.png");
  } else if (pais.equals("Brasil")) {
    mapabase=loadImage("Brasil.png");
  } else if (pais.equals("Canada")) {
    mapabase=loadImage("Canada.png");
  } else if (pais.equals("Chile")) {
    mapabase=loadImage("Chile.png");
  } else if (pais.equals("Costa Rica")) {
    mapabase=loadImage("Costa Rica.png");
  } else if (pais.equals("Cuba")) {
    mapabase=loadImage("Cuba.png");
  } else if (pais.equals("Ecuador")) {
    mapabase=loadImage("Ecuador.png");
  } else if (pais.equals("Espania")) {
    mapabase=loadImage("Espania.png");
  } else if (pais.equals("Estados Unidos")) {
    mapabase=loadImage("Estados unidos.png");
  } else if (pais.equals("Estados unidos")) {
    mapabase=loadImage("Estados unidos.png");
  } else if (pais.equals("Mexico")) {
    mapabase=loadImage("Mexico.png");
  } else if (pais.equals("Panama")) {
    mapabase=loadImage("Panama.png");
  } else if (pais.equals("Portugal")) {
    mapabase=loadImage("Portugal.png");
  } else if (pais.equals("Trinidad y Tobago")) {
    mapabase=loadImage("Trinidad.png");
  } else if (pais.equals("Uruguay")) {
    mapabase=loadImage("Uruguay.png");
  } else if (pais.equals("Venezuela")) {
    mapabase=loadImage("Venezuela.png");
  }
}

//void loadDataInBackgroundImage(String Data) {

//  if (Data.equals("Colombia")) {
//    mapabase=loadImage("Colombia.png");
//  } else if (pais.equals("Argentina")) {
//    mapabase=loadImage("Argentina.png");
//  }
//}


void draw() {

  PVector mp = new PVector(mouseX, mouseY);

  image(mapabase, 0, 0);
  text("Inversión en ACTI como porcentaje del PIB según países seleccionados, 2003 - 2012", 50, 40);
  textFont(titles, 10);
  text("Fuentes: Para Colombia OCyT, para el resto de países RICyT.", 680, 40);
  text("Cálculos: OCyT.", 680, 55);
  int i=yearSelected;


  if (i >= 0) {

    for (TableRow row : tabla.rows()) {
      int id= row.getInt("id");
      //float anio12=row.getFloat("2012");
      //println(row.getString("Pais"));  // Prints "Mosquito"
      //row.setString("2003", "Ladybug");

      int cdX=row.getInt("cordx");
      int cdY=row.getInt("cordy");
      float valor=row.getFloat(2000+i+3+"");
      String ano=2000+i+3+"";


      PVector cp = new PVector(cdX, cdY);

      float d = cp.dist(mp);
      if (d < valor*10) {
        println("I am inside the circle! d = " + d); 
        String pais = row.getString("Pais");
       
        loadInNewBackgroundImage(pais);
        yearSelected = -1;


        //printInterestingData(pais);

        println(pais); 
        fill(255, 0, 0);
      } else {
         
        fill(255, 255, 50);
      } 

      ellipse(cdX, cdY, valor*10, valor*10);

      fill(0);
      String values= row.getString(2000+i+3+"");

      fill(60);
      textFont(numbers, 10);
      text(values, cdX, cdY);

//rect(890,50,30,20);
//rect(cdX, cdY, 10, 10);
    }
 //fill(255, 255, 0);
 //ellipse(302, 395, 7, 7);
  }//cierro primer for

  for (int number=0; number < 10; number++) {
    textFont(titles);
    fill(100);
    text(anios[number], (number+1)*90, 600);
    for (int boton=0; boton < 10; boton++) {
      noStroke();
      fill(102, 50, 80);
      rect((boton+1.1)*90, 570, 10, 10);
      
      
    }//cierro primerfor
  }///cierro segundofor

  //println("-------------------------------------------");
}//cierro draw

boolean overRect(float x, float y, int width, int height) {
  if (mouseX >= x && mouseX <= x+width && 
    mouseY >= y && mouseY <= y+height) {
    return true;
  } else {
    return false;
  }
}

void mouseMoved() {

  for (int i=0; i<10; i++) {
    if (overRect((i+1.1)*90, 570, 10, 10)) {
      yearSelected = i;
    }
      
      }   
  }
  
