Notatki
=======

- (content->serviceRel),  nie ma rzeczy uniwersalnych, per plaikacja: content_count i content_id, zapis content_id_img
- (content->service) zapis recursive replace przez service
- paramsy z wartosciami dla contentu lub jako flagi bez wartosci,klucz 255 i wartosc text, jako osobna tabela
- zawsze przekazywac model danych entity nie musi byc pelny ale zawsze entity



i joiny dla contentRel + contentinbox count = how?


petFootrprint jhak to powinno byc zrobione?
 
- lista footprintow pogrupowana dla obrazka peta
- ostatni footprint


- dodatkowa walidacja przez event w c_Admin_article, podlaczanie sie pre i post przy akcjach na contencie




listy sortowane dla danego modulu
czyli w c_admin_costam mozna wlaczyc order reczny po polu costam_order
nie robic tego tylko to opisac



404 notfound


----------------

przetestowac:
admin_form
module_admin_plugin_formCancel
module_admin_plugin_saveAndClose


module_content_service_rel

zadania:

- add 1 dodac nowego slave: z orderem MAX+1
  $this->module->content->serviceRel->addSlave($master, $slave[, 'img'], $order = null);
  $this->module->content->serviceRel->addSlave($master, $slave[, 'img'], $order = null);
- add 8 zdefiniowac nowe relac
  $this->module->content->serviceRel->setSlaves($master, $slaves[, 'img'], $order = null);

- remove 1
  $this->module->content->serviceRel->removeSlave($master, $slave[, 'img'])
- remove 8
  $this->module->content->serviceRel->removeSlaves($master, $slaves[, 'img'])
  $this->module->content->serviceRel->removeAllSlaves($master, 'img')

  
- move 1 before
  $this->module->content->serviceRel->moveBefore($master, $slave, $beforeSlave[, 'img']);
- move 1 after
  $this->module->content->serviceRel->moveBefore($master, $slave, $afterSlave[, 'img']);

- zapis pierwszego do content_id_content_img
  $this->module->content->serviceRel->setMainRel($master, $slave, 'content_id_content_img')

- zapis counta - na zasadzie oblicz
  $this->module->content->serviceRel->setCountByCalculation(master, 'img', 'content_count_content_img')

- zapis counta --
  $this->module->content->serviceRel->setCountByIncrement(master, 'img', 'content_count_content_img')

- zapis counta ++
  $this->module->content->serviceRel->setCountByIncrement(master, 'img', 'content_count_content_img')

$this->module->content->serviceOrder->saveOrder($content_type, $aNewOrder);
  
  
- pobieranie slave
- pobieranie masterow

array('contentRel_id_content_master' => 13, contentRel_type 'img');





wyjatkowe artykuly
 
content_list = 'yes' | 'no' DEFAULT yes

z robotsami inaczej pracowac

$this->module->content->service->fetchAllByIdsAndOrder($aIds);

- wlasciowosc htmlmeta
- contentOriginBan

- bledy na tiere: content_id_user a powinno byc content_id_profile



$this->module->article->repository->fetchAll(array(
	'contentRel_id_content_slave' => $tree_id,
));



------------------------------------------------

Mozna stworzyc metody w podstawowym serwisie typu 

```
module_article_service->beforeSave(array &$entity)
                      ->afterFetch(array &$entity)
```

i je odpalac
