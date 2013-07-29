TODO
====
 
3. module_content_operation
{
    savePre(array $entity);
    savePost(array $entity);
    fetchPost(array $entity);
    removePre();
    removePost();
}
$this->module->content->operation->savePre($entity);
$this->module->content
zrobic pseudo implementacje: count, content_id_content_tree, parowanie body, indeksowanie dla wyszukiwarka
flaga _new entity
$this->module->content->rel->saveRef($entity, 'content_id_content_tree', $entity['contentRelation']['tree'][0]);
 
4. obsluga drzewa module_tree_tree
{
    module() { return f::$c->module->tree; }
    getAll();
    getTree();
    getTitle($id)
    get{Cos}By{Cos_innego_iz_id}
    getLocation($id)
    getLocationPaths($id);
    getSibling($id);
    getSiblingPaths($id);
    getChild($id);
    getIdsRecursive(array $aTreeIds)
 
    isCurrent();
    isParrent();
    setCurrent(); // ustawia current i parrent
    getCurrent(); // module_tree_serviceTreeNode
    getParent();  // module_tree_serviceTreeNode
 
}

module_tree_treeNode
{
    is();
    getId();
    getTitle();
    getLocation(); {return $tree->getLocation($this->getId()); }
    getChild();
}
 
$this->tree        = $this->module->tree->tree;
$this->treecurrent = $this->module->tree->tree->getCurrent();
$this->treeparent  = $this->module->tree->tree->getParent();
 
5. indeksowanie i szukanie
- cos jak na gastro`
- contentSearchWord
- contentSearch: id_content id_contentSearchWord
- content_search_update
- content_search_checksum
- module_content_repository_interface->entity2search($entity) { // dodac do interface
    $search = array();
    each submodule ->entity2search($entity, $search)
    $this->_entity2search($entity, $search)
}
array(
    '',
    '',
    '',
)
- $this->module->content->search->index($entity);
- $this->module->content->search->indexAll()
- dodanie szukania do wszystkich entity danego typu
- fetch(array(
    'contentSearch'          => 'Ala ma kota'
    'contentSearch_operator' => 'AND' // operator logiczny AND OR, default AND
));
 
6. $this->module->content->service->saveRecursiveByRelation($entity, $contentRelation_type, array $data)
{
    $update = array(); // ustawic content_id lub content_origin
    $update += $data;
 
    $id = $this->module->content->save($update); // jezeli nei bylo content_id to go dostaniemy
 
    foreach (
        $this->module->content->fetchAll(array(
            'contentRelation_id_content_master' => $id,
            'contentRelation_type'              => $contentRelation_type,
            'order'                             => contentR..._order
        ))
        as $slave
    ) {
        $this->saveRecursiveByRelation(array('content_id' => $slave['content_id']), $contentRelation_type, $data);
    }
}
 
7. comment to content czy nie? jezeli da sie obsluzyc przez fetcher() i pozniej tuples2entities() to nie musi byc contentem
 
8. $this->module->content->service->fetchAllKeyedByIdsAndOrder($aIds); i podmienic w module_content_subcontent_contentRelated i chyba tez jest w module_content_repository->fetchAll()
 
9. ACL do drzewa

Best practice
=============
 
- zawsze przekazywac model danych entity nie musi byc pelny ale zawsze entity
- pisac uniwersalne funkcje np. saveRecursiveByRelation - dowolnya relacja, dowolny typ danych
- standardowe widoki - proste, na cala szerokosc, brak sliderow, brak paginacji ...
- z robotsami inaczej pracowac
- bledy na tiere: content_id_user a powinno byc content_id_profile
 
 
Notatki
=======
 
- petFootrprint jhak to powinno byc zrobione?
- lista footprintow pogrupowana dla obrazka peta
- ostatni footprint
- dodatkowa walidacja przez event w c_Admin_article, podlaczanie sie pre i post przy akcjach na contencie
- listy sortowane dla danego modulu czyli w c_admin_costam mozna wlaczyc order reczny po polu costam_order
  nie robic tego tylko to opisac
- acl do wezla w drzewie
- feature
- admin pluginy: admin_form, module_admin_plugin_formCancel, module_admin_plugin_saveAndClose
- przygotowac sie na site
- module->content->rel i counter
    - zapis counta - na zasadzie oblicz
      $this->module->content->serviceRel->setCountByCalculation(master, 'img', 'content_count_content_img')
    - zapis counta --
      $this->module->content->serviceRel->setCountByIncrement(master, 'img', 'content_count_content_img')
    - zapis counta ++
      $this->module->content->serviceRel->setCountByIncrement(master, 'img', 'content_count_content_img')
- wyjatkowe artykuly content_list = 'yes' | 'no' DEFAULT yes
- wlasciowosc htmlmeta
- contentOriginBan
 
saveCountByCalculationFromChild
 
operacje
 
count
content_count_content_img; img;
 
ref
content_id_content_img; img, 0