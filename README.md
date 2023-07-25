entetes_colonnes = ['Prénom & Nom', 'Département', 'Matière', 'Diplôme', 'Niveau', 'Type', 'Période', 'Cours (heures)', 'Cours (groupes)', 'Cours (semaines)', 'TD (heures)', 'TD (groupes)', 'TD (semaines)', 'TP (heures)', 'TP (groupes)', 'TP (semaines)', 'Cintgr (heures)', 'Cintgr (groupes)', 'Cintgr (semaines)', 'CIN']
tableau_entree_1 = [
    ['Majdi Argoubi', 'Anglais', 'TVA', 'Licence', '1', 'Sciences', 'S1', '0', '0', '14', '11', '1', '14', '0', '0', '14', '0', '0', '14', '10'],
    ['x', 'Finance', 'TVA', 'Licence', '1', 'Sciences', 'S1', '0', '0', '14', '11', '2', '14', '0', '0', '14', '0', '0', '14', '12'],
    ['y', 'Comptabilité', 'TVA', 'Licence', '1', 'Sciences', 'S2', '0', '0', '14', '11', '2', '14', '0', '0', '14', '0', '0', '14', '13'],
    ['z', 'Economie', 'TVA', 'Licence', '1', 'Sciences', 'S2', '0', '0', '14', '11', '2', '14', '0', '0', '14', '0', '0', '14', '11'],
    ['Majdi Argoubi', 'Anglais', 'TVA', 'Licence', '1', 'Sciences', 'S2', '0', '0', '14', '11', '1', '14', '0', '0', '14', '0', '0', '14', '10'],
]
entetes_colonnes_2 = ['CIN', 'RIB', 'Grade', 'الاسم و اللقب', 'Spécialité', 'Statut', 'Etablissement d\'origine', 'Grade dans l\'Etablissement d\'origine', 'Dernier Diplôme Obtenu', 'Due Cours', 'Due TD', 'Due TP']
tableau_entree_2 = [
    ['10', '12454556', 'Assistant', '', 'x7', 'Permanant', '', '', '', '0', '11', '0'],
    ['11', '12454556', 'Contrat Docteur', '', 'x7', 'Permanant', '', '', '', '0', '9.5', '0'],
    ['12', '12454556', 'Assistant', '', 'x7', 'Permanant', '', '', '', '0', '0', '0'],
    ['13', '12454556', 'Professeur', '', 'x7', 'Permanant', '', '', '', '5.5', '0', '0'],
]
def verif_conditions(tableau1, tableau2):
    cin_nom_dict = {}
    cin_dept_dict = {}  
    cin_count_dict = {} 
    cin_multi_nom = {}  
    cin_multi_dept = {}  
    erreurs = []  
    for ligne1 in tableau1:
        cin = ligne1[-1]  
        nom = ligne1[0]
        dept = ligne1[1]
        if cin in cin_nom_dict and cin_nom_dict[cin] != nom:
            if cin not in cin_multi_nom:
                cin_multi_nom[cin] = [cin_nom_dict[cin]]
            cin_multi_nom[cin].append(nom)
            erreurs.append(f"- Le N° CIN={cin} est associé à plusieurs 'Prénom & Nom': {', '.join(cin_multi_nom[cin])}. Merci de vérifier.")
        if cin in cin_dept_dict and cin_dept_dict[cin] != dept:
            if cin not in cin_multi_dept:
                cin_multi_dept[cin] = [cin_dept_dict[cin]]
            cin_multi_dept[cin].append(dept)
            erreurs.append(f"- Le N° CIN={cin} est associé à plusieurs 'Département': {', '.join(cin_multi_dept[cin])}. Merci de vérifier.")
        cin_nom_dict[cin] = nom  
        cin_dept_dict[cin] = dept
    for ligne2 in tableau2:
        cin = ligne2[0]  
        if cin not in cin_nom_dict:
            erreurs.append(f"- Le N° CIN={cin} n'est associé à aucun enseignant. Merci de vérifier.")
        cin_count_dict[cin] = cin_count_dict.get(cin, 0) + 1
    for cin, count in cin_count_dict.items():
        if count >= 2:
            erreurs.append(f"L'enseignant {cin_nom_dict[cin]} (CIN : {cin}) a plusieurs lignes de données dans le tableau 2. Merci de vérifier.")
    for cin, nom in cin_nom_dict.items():
        if cin not in cin_count_dict:
            erreurs.append(f"L'enseignant {nom} (CIN : {cin}) n'a pas de données dans le tableau 2. Merci de vérifier.")
    if erreurs:
        print("Des erreurs ont été détectées. Veuillez vérifier vos données.")
        for erreur in erreurs:
            print(erreur)
        raise SystemExit
    print("Vos données sont ok !!!")
verif_conditions(tableau_entree_1, tableau_entree_2)
![image](https://github.com/medinacity/streamlit-example/assets/140558828/0c3ba41e-5461-45e6-92dc-48d43935c999)
