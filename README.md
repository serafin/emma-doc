Dokumentacja do EMMA (Elasytczna MikroModułowa Architektura) - szkielet z podstawowymi modulami i funkcjami

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