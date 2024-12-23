# Progetto-Python
In questo repository è presente il progetto Python di Romar Martin

# Funzione per aggiungere una nuova ricetta alla lista
def aggiungi_ricetta(lista_ricette):
# Chiediamo all'utente di inserire il nome della ricetta
    
    nome = input("Inserisci il nome della ricetta da aggiungere: ")
    
# Verifica se la ricetta è già presente nella lista
    for ricetta in lista_ricette:
        if ricetta["nome"].lower() == nome.lower():            # Confronto del nome ignorando maiuscole/minuscole
            print(f"La ricetta {nome} esiste già.")            # Se la ricetta esiste già, informiamo l'utente
            return                                             # Uscita dalla funzione se la ricetta è già presente

# Chiediamo all'utente di inserire gli altri dettagli della ricetta
    categoria = input("Inserisci la categoria della ricetta (es. antipasto, primo, dolce): ")
    ingredienti = input("Inserisci gli ingredienti separati da virgola: ").split(",")            # Istruzione per separare gli ingredienti con una virgola
    tempo = int(input("Tempo di preparazione (minuti): "))                               # Richiesta del tempo di preparazione in minuti
    
# Creiamo un dizionario con tutte le informazioni della nuova ricetta
    nuova_ricetta = {
        "nome": nome,
        "categoria": categoria,
        "ingredienti": [ingrediente.strip() for ingrediente in ingredienti],        # Rimuoviamo spazi vuoti prima e dopo ogni ingrediente
        "tempo": tempo
    }
# Aggiungiamo la nuova ricetta alla lista
    lista_ricette.append(nuova_ricetta)
    print(f"La ricetta {nome} è stata aggiunta correttamente.")    # Conferma dell'aggiunta
    print(nuova_ricetta)
#_____________________________________________________________________________________________
# Funzione per visualizzare tutte le ricette
def visualizza_ricette(lista_ricette):
# Cicliamo su tutte le ricette presenti nella lista e le visualizziamo

    for ricetta in lista_ricette:
        print(f"Nome: {ricetta['nome']}")
        print(f"Categoria: {ricetta['categoria']}")
        print(f"Ingredienti: {', '.join(ricetta['ingredienti'])}")         # Mostriamo gli ingredienti separati da virgola
        print(f"Tempo: {ricetta['tempo']} minuti")                         # Mostriamo il tempo di preparazione
        print("-" * 30)                                                    # Separatore per ogni ricetta
#______________________________________________________________________________________________

# Funzione per cercare ricette in base a diversi attributi
def cerca_ricetta(lista_ricette):
# Mostriamo le opzioni di ricerca per nome, categoria, ingrediente o tempo
    print("1) Cerca per nome")
    print("2) Cerca per categoria")
    print("3) Cerca per ingrediente")
    print("4) Cerca per tempo")
    
# Chiediamo all'utente di scegliere quale opzione usare per la ricerca
    scelta = input("Scegli una opzione (1-4): ")
    
    if scelta == '1':                                     # Ricerca per nome
        nome = input("Nome della ricetta: ")
        for ricetta in lista_ricette:
            if nome.lower() in ricetta["nome"].lower():             # Controlliamo se il nome cercato è nel nome della ricetta
                visualizza_ricette([ricetta])                       # Mostriamo le ricette che corrispondono
    elif scelta == '2':                                             # Ricerca per categoria
        categoria = input("Categoria della ricetta: ").lower()
        for ricetta in lista_ricette:
            if categoria in ricetta["categoria"].lower():       # Controlliamo se la categoria corrisponde
                visualizza_ricette([ricetta])                   # Mostriamo le ricette che corrispondono
    elif scelta == '3':                                         # Ricerca per ingrediente
        ingrediente = input("Ingrediente da cercare: ").lower()
        for ricetta in lista_ricette:
            if any(ingrediente in ing.lower() for ing in ricetta["ingredienti"]):  # Controlliamo se l'ingrediente è presente nella lista degli ingredienti
                visualizza_ricette([ricetta])                                      # Mostriamo le ricette che corrispondono
    elif scelta == '4':                                                            # Ricerca per tempo
        tempo = int(input("Tempo di preparazione (minuti): "))
        for ricetta in lista_ricette:
            if ricetta["tempo"] == tempo:                                          # Controlliamo se il tempo di preparazione è uguale
                visualizza_ricette([ricetta])                                      # Mostriamo le ricette che corrispondono
    else:
        print("Scelta non valida. Riprova.")                                       # Se la scelta non è valida, chiediamo di riprovare
        cerca_ricetta(lista_ricette)                                               # Riproviamo la ricerca
#______________________________________________________________________________________________

# Funzione per mostrare la frequenza di un ingrediente nelle ricette
from collections import Counter
def statistiche_ingrediente(lista_ricette):
    if not lista_ricette:                                       # Verifica se la lista delle ricette è vuota
        print("La lista delle ricette è vuota.")
        return
    
# Estraiamo tutti gli ingredienti e li mettiamo in una lista
    tutti_ingredienti = [ingrediente.lower() for ricetta in lista_ricette for ingrediente in ricetta["ingredienti"]]
    
# Chiediamo all'utente di inserire un ingrediente per verificare quante volte appare
    ingrediente_cercato = input("Ingrediente da cercare: ").strip().lower()
    conteggio = Counter(tutti_ingredienti)  # Contiamo quante volte ogni ingrediente appare nella lista
    
# Mostriamo il numero di ricette che contengono l'ingrediente cercato
    print(f"L'ingrediente '{ingrediente_cercato}' appare {conteggio.get(ingrediente_cercato, 0)} volte.")
#______________________________________________________________________________________________

# Funzione per filtrare le ricette con due ingredienti specifici
def filtraggio_avanzato(lista_ricette):
# Chiediamo all'utente di inserire due ingredienti
    ingrediente1 = input("Primo ingrediente: ").lower()
    ingrediente2 = input("Secondo ingrediente: ").lower()
    
# Filtra le ricette che contengono entrambi gli ingredienti
    ricette_filtrate = [
        ricetta for ricetta in lista_ricette
        if ingrediente1 in [ing.lower() for ing in ricetta["ingredienti"]] and
           ingrediente2 in [ing.lower() for ing in ricetta["ingredienti"]]
    ]
    
    if ricette_filtrate:                               # Se ci sono ricette che corrispondono, le mostriamo
        visualizza_ricette(ricette_filtrate)
    else:                                              # Se non ci sono ricette che corrispondono, informiamo l'utente
        print(f"Nessuna ricetta trovata con '{ingrediente1}' e '{ingrediente2}'.")
#______________________________________________________________________________________________

# Lista di ricette predefinite
lista_ricette = [
    {"nome" : "Bruschette al pomodoro", "categoria" : "antipasto", "ingredienti" : ["Pane casereccio", "pomodori", "basilico fresco", "aglio", "olio extravergine di oliva", "sale", "pepe"], "tempo" : 15} ,
    {"nome" : "Caprese di mozzarella e pomodoro", "categoria" : "antipasto", "ingredienti" : ["Mozzarella di bufala", "pomodori maturi", "basilico fresco", "olio extravergine di oliva", "sale", "pepe"], "tempo" : 10} ,
    {"nome" : "Carpaccio di zucchine", "categoria" : "antipasto", "ingredienti" : [ "Zucchine", "parmigiano a scaglie", "olio extravergine di oliva", "succo di limone", "sale", "pepe"], "tempo" : 10} ,
    {"nome" : "Crocchette di patate" , "categoria" : "antipasto" , "ingredienti" : ["Patate", "uova", "parmigiano grattugiato", "pangrattato", "sale", "pepe", "olio per friggere"], "tempo" : 40} ,
    {"nome" : "Spaghetti alla carbonara", "categoria" : "primo piatto", "ingredienti" : ["Spaghetti", "guanciale", "uova", "pecorino romano", "pepe nero"], "tempo" : 30} ,
    {"nome" : "Risotto allo zafferano", "categoria" : "prima piatto", "ingredienti" : ["Riso Carnaroli", "cipolla", "brodo vegetale", "zafferano", "burro", "parmigiano grattugiato", "sale"], "tempo" : 25} ,
    {"nome" : "Pasta al pesto genovese", "categoria" : "primo piatto", "ingredienti" : ["Pasta", "basilico fresco", "olio extravergine di oliva", "parmigiano grattugiato", "pinoli", "aglio", "sale"], "tempo" : 8} ,
    {"nome" : "Cacio e pepe", "categoria" : "primo piatto", "ingredienti" : ["Pasta", "pecorino romano", "pepe nero", "acqua di cottura"], "tempo" : 15} ,
    {"nome" : "Pollo alla cacciatora", "categoria" : "secondo piatto", "ingredienti" : ["Pollo a pezzi", "cipolla", "carota", "sedano", "passata di pomodoro", "olive nere", "olio extravergine di oliva", "rosmarino"], "tempo" : 60} , 
    {"nome" : "Salmone al forno con erbe", "categoria" : "secondo piatto", "ingredienti" : ["Filetto di salmone", "olio extravergine di oliva", "limone", "rosmarino", "timo", "sale", "pepe"], "tempo" : 30, "costo" : 13} , 
    {"nome" : "Parmiagiana di melanzane", "categoria" : "secondo piatto", "ingredienti" : ["Melanzane", "passata di pomodoro", "mozzarella", "parmigiano grattugiato", "basilico", "olio extravergine di oliva", "sale"], "tempo" : 50} , 
    {"nome" : "Frittata di zucchine", "categoria" : "secondo piatto", "ingredienti" : ["Uova", "zucchine", "parmigiano grattugiato", "olio extravergine di oliva", "sale", "pepe"], "tempo" :  25} , 
    {"nome" : "Verdure grigliate", "categoria" : "contorno", "ingredienti" : ["Zucchine", "melanzane", "peperoni", "olio extravergine di oliva", "sale", "pepe"], "tempo" : 8} , 
    {"nome" : "Piselli al burro", "categoria" : "contorno", "ingredienti" : ["Piselli freschi o surgelati", "burro", "cipolla", "sale", "pepe"], "tempo" : 7} , 
    {"nome" : "Panna cotta al caramello", "categoria" : "dolci", "ingredienti" : ["Panna fresca", "zucchero", "gelatina in fogli", "estratto di vaniglia", "caramello"], "tempo" : 15} , 
    {"nome" : "Crostata di marmellata", "categoria" : "dolci", "ingredienti" : ["Farina", "burro", "zucchero", "uova", "lievito per dolci", "marmellata a scelta"], "tempo" : 50} ,
    {"nome": "Boeuf Bourguignon", "categoria": "secondo", "ingredienti": ["Manzo", "vino rosso", "cipolle", "carote", "funghi", "pancetta", "aglio", "alloro", "timo", "concentrato di pomodoro", "farina", "brodo"], "tempo": 180}
]
#______________________________________________________________________________________________

# Funzione principale che gestisce il menu del programma
def avvia_programma():
    while True:                       # Il programma continua a girare finché l'utente non decide di uscire
        print("\nIndice:")
        print("1) Visualizza ricette")
        print("2) Aggiungi ricetta")
        print("3) Cerca ricetta")
        print("4) Statistiche ingredienti")
        print("5) Filtraggio avanzato")
        print("6) Esci")
        
# Chiediamo all'utente di scegliere un'opzione
        scelta = input("Scegli un'opzione (1-6): ")
        
# Eseguiamo l'operazione scelta
        if scelta == '1':
            visualizza_ricette(lista_ricette)
        elif scelta == '2':
            aggiungi_ricetta(lista_ricette)
        elif scelta == '3':
            cerca_ricetta(lista_ricette)
        elif scelta == '4':
            statistiche_ingrediente(lista_ricette)
        elif scelta == '5':
            filtraggio_avanzato(lista_ricette)
        elif scelta == '6':                       # Se l'utente sceglie di uscire, terminiamo il programma
            print("Arrivederci!")
            break
        else:
            print("Opzione non valida. Riprova.")    # Se la scelta non è valida, chiediamo di riprovare
#______________________________________________________________________________________________

# Avvio del programma
avvia_programma()
