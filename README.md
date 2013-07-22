EMMA - dokumnetacja 
===================

EMMA - Elasytczna MikroModułowa Architektura.

Szkielet z podstawowymi modulami i funkcjami.


Wersja - v2
-----------

- atomicznosc repozytoriow, repozytoria zapisuja tylko swoje wlasne entity, prosty zapis danych,
  w zapisie zadnych odwolan do zewnetrznych kosztownych operacji
- tree jest teraz contentem, drzewo budowane jest na zasadzie relacji contentowych tree-tree,
  polaczenie contetow z tree przez polaczenie wezlow drzewa z contentem (tak jak obrazki do artykulu)
- uproszczono importy
- skalowalnosc subcontentow, wydzielona warstwa subcontentow, 
  mozna w prosty sposob dopisac nowy reuzywalny subcontent i w prosty sposob podlaczyc pod dowolne contenty
- ulepszone relacje contentow i dane relacji
- wersjonowanie cotentow - dvc
- indeksowanie danych dla wyszukiwania
- laczenie contentow z innymi modelami nie contentowymi


Warstwy architektury 
--------------------

- moduly `module_interface`
- service'sy
- repozytoria contentowe `module_content_repository_interface` np. article, gallery, img
  - subcontenty `module_content_subcontent_interface` np. location, contact, htmlmeta
- importy
  - inputy `module_import_input_interface`
  - importer `module_import_importer`
  - task - model `m_import` i service `module_import_task`
- admin
- front - activity i view
