Reflekter kort men fagligt over din løsning med henblik på udfordringerne og successerne ved opgaven.

I fobindelse med at løse denne opgave har jeg under vejs stødt på mange udfordringer. Den største har været at få main layotet til at fungere ordenligt, så siderne blev ens og alt indholdet lagde sig indefor en bredde på 1200px. For at løse det problem har jeg prøvet mange forskellige layout teknikker af, og eksperimenteret med hvor jeg skulle placere dem i min filestruktur. Min første indskydelse var at skrive koden i min Global CSS file, men konkluderet det hurtigt at det rent vedligholdsmæssigt gav bedre mening at skrive den i et Layout component, da det er et layout der skal gå igen over alle siderne. Efterfølgende har mine udfordringer mere været, at gennemskue min HTML struktur, og få de forskellige container og elementer til at agerer efter main layoutet.

Optur ved projektet
De gange jeg har haft mere optur har været i forhold til at fetche data fra projektet tilhørende API. Den process er for mig meget naturlig, efter som har man først fået det til at virke en gang er det bare bare at skifte endpoints ud, når du skal fetche data til en ny del i projektet. En anden ting der for mig også har været en optur, er at mange af de udfordringer jeg har er stødt på undervejs har jeg gennem eksperimentering og ved at google nået frem til en løsning.

nedstående kodestump er den kodestump der har voldet meget størst udfordringer, men også den der er grundstenen for alle sidernes layout.
Jeg har gjort brug af en layout teknik, hvor jeg har kunne definerer et grid med en indholdsbredde på 1200px og et fragment (1fr) i hver side. Dette har gjort at alt sidens indhold har lagt sig i midten, med mindre man har defineret det skulle udnytte den fulde bredde af viewporten ved brug af klassen ".full" Ydermere koden læsbar for andre, da gridlinjerne er navngivet i stedet for at havde et tal.

Layoutet indeholder også en klasse kaldt ".flow-space1" som bliver brugt til at skabe en afstand/luft i layoutet.

body{
--gap: clamp(1rem, 6vw, 22.5rem);
--full: minmax(var(--gap), 1fr);
--content: min(75rem, 100% - var(--gap) \* 2);
--feature:0;

    display: grid;
    grid-template-columns: [full-start] var(--full) var(--feature) [content-start] var(--content) [content-end]
    var(--full)[full-end];


    > * {
    grid-column: content;

}

.flow-space{
&{
margin-block-start: var(--flow-space1, 4rem);
}

}
.full {
grid-column: full;
display: grid;
grid-template-columns: subgrid;
}
}

I mit arbejde med dette projekt har jeg tænkt meget I hvordan jeg kunne organisere mine variabler og generelt min stylling af de forskellige dele i koden.

Jeg havde som udgangspunkt fire CSS filer reset.css, global.css, components.css og overrides.css som alle var specificeret som @layers. Jeg fandt det hurtigt forvirrende at havde så mange CSS filer, så endte med at skrotte overrides.css da jeg hurtigt indså at jeg havde givet min global CSS dens formål.

Så min fremgangsmåde har kort sagt været, som følgende:
-global.css indeholder alle de globale costume variabler, som jeg bruger på kryds og tværs i projketet og samtidig har jeg også defineret et override på alle de elementer jeg har brugt.

-component.css indeholder mange af de stylingsregler der kun skal gælde componenter.

-stylling lokalt, hvor jeg har stylet componenterne lokalt.

reflektion:
Når jeg ser tilbage på processen, er der nogle ting jeg vil gøre anderledes i fremtiden.

1. Jeg indså alt for sent at jeg ville havde kunne spare noget kode, ved at gøre brug af data attributter, dette ville havde løst mange af de tilfælde hvor jeg havde container med forskellige baggrundsfarver. Her havde det været nemmere at gøre det frem for at definere en class til hver container og give den class en baggrundsfarve.

2. At havde skrevet mere af component styllingen i den globale css frem for lokalt på componentet, da mange af de samme værdier går igen på de forskellige componenter.
   Her indså jeg også for sent at jeg skulle havde lavet et cardlayout component, da der flere gange i designet indgik cards.

3. Definere de mest gængese layout-patterns som data atrributter, så de er defineret et sted frem for under hvert component eller side man laver.
