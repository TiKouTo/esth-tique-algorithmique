//set up classe 
il faut que la classe contienne la densité du tableau (entier entre 0 et 1 = proba placer un point noir)
je propose :
-high density=0.9
-mediem d=0,7
-low d=0,5
-super low d=0,3 

la classe doit aussi contenir un autre tableau

les objets de la classe seront nommés au pif disont tab; 

//set up tableaux de données
la taille de l'écran :x=3*4^4=768   ; y=2*4^4=512
let screen=[];
let tab ; // objet avec la classe 
for i in range 16
{
    screen.push(tab);
}

// on créer tout les éleements de screen : 
let tabdensity=[0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.7,0.7,0.7,0.5,0.5,0.3] // 10 high density, 3 medium, 2 low, 1 super low;
let tailletabdensityrandom=16;

screen.forEach(function(item, index, array) {

    //on pick au hasard quel densité dans le tabdensity on va prendre;
    let tabdensityrandom = random(16);
    let removedItem = tabdensityrandom.splice(tabdensityrandom, 1);
    tailletabdensity--;// est ce qu'il connait tailletabdensity puisqu'on est dans la fonction,ou il faut que je le rajoute en argument? 
    item.density=removedItem;
    let superfield=[];
    item.next=superfield;
    

    // on répète pour superfield : 
    let tab ; // est ce que tab est déjà déclaré vu qu'on est dans une fonction ? 
    for i in range 16
    {
        superfield.push(tab);
    }

    // on créer tout les éleements de superfield : 
    let tabdensity=[0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.7,0.7,0.7,0.5,0.5,0.3]
    let tailletabdensityrandom=16;

    superfield.forEach(function(item, index, array) {

        let tabdensityrandom = random(16);
        let removedItem = tabdensityrandom.splice(tabdensityrandom, 1);
        tailletabdensity--;
        item.density=removedItem;
        let largefield=[];
        item.next=largefield;
        
        let tab ;
        for i in range 16
        {
            largefield.push(tab);
        }

        let tabdensity=[0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.7,0.7,0.7,0.5,0.5,0.3]
        let tailletabdensityrandom=16;

        largefield.forEach(function(item, index, array) {

            let tabdensityrandom = random(16);
            let removedItem = tabdensityrandom.splice(tabdensityrandom, 1);
            tailletabdensity--;
            item.density=removedItem;
            let smallfield=[];
            item.next=smallfield;

            let tab ;
            for i in range 16
            {
                smallfield.push(tab);
            }

            let tabdensity=[0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.7,0.7,0.7,0.5,0.5,0.3]
            let tailletabdensityrandom=16;

            smallfield.forEach(function(item, index, array) {

                let tabdensityrandom = random(16);
                let removedItem = tabdensityrandom.splice(tabdensityrandom, 1);
                tailletabdensity--;
                item.density=removedItem;
                
                let module=[];
                item.next=module;

                //dans chaque module il y a 6 pixels mais chaque pixel à la même proba d'être noir

            });
        });
    });
});


//parcours les tableaux pour dessiner les points 
let x=0;
let y=0;
for i1 in range 16 //parcours l'écran = le tableau de superfields 
{
    for i2 in range 16 //parcours le tab de large fields
    {
        for i3 in range 16  // small fields
        {
            for i4 in range 16  //modules
            {
                for i5 in range 6 // pixels
                {
                    //set up probabilité de placer un point noir ; pour info avec les choix de densité pmax=2/3 et correspond à 15% des pixels :
                    f1=screen[i1];//superfield 
                    f2=f1.next[i2];//largefield
                    f3=f2.next[i3];//smallfield
                    f4=f3.next[i4];//module
                    p= f1.density * f2.density * f3.density * f4.density

                    //set up x et y : 
                    les i parcourent le tableau selon x et y donc il faut les %4; pcq le 5 eme element du tableau est placé au même x que le 1er; 
                    
                    x=192*(i1%4)+48*(i2%4)+12*(i3%4)+3*(i4%4)+i5%3;
                    y=128*(i1%4)+32*(i2%4)+8*(i3%4)+2*(i4%4)+i5%2;

                    placernoirbool=random(1000);
                    if(placernoirbool<(p*1000)){
                        let c= color(0,0,0) // il faudra ajouter un back blanc
                        fill(c);
                        noStroke();
                        rect(x, y, 1, 1);
                    }   
                }
            }
        } 
    }

}
