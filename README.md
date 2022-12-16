# Worked

select
       sos.store_number,
       sos.shelf_out_session, sos.thd_fiscal_week, so.shelf_out_id,
       (so.aisle || '-' || so.bay) as aisle_bay, sku_number, so.department, so.class_number,
                             q.question, a.answer

 from pr-store-merch-thd.STORE_BAY_INTEGRITY.SHELF_OUT_QUESTION_ANSWER as soqa

 join pr-store-merch-thd.STORE_BAY_INTEGRITY.SHELF_OUT as so

       on soqa.shelf_out_id = so.shelf_out_id
  
join pr-store-merch-thd.STORE_BAY_INTEGRITY.SHELF_OUT_SESSION sos

      on so.shelf_out_session_id = sos.shelf_out_session_id

join pr-store-merch-thd.STORE_BAY_INTEGRITY.QUESTION_ANSWER qa

      on soqa.question_answer_id = qa.question_answer_id

join pr-store-merch-thd.STORE_BAY_INTEGRITY.ANSWER a

      on qa.answer_id = a.answer_id

join pr-store-merch-thd.STORE_BAY_INTEGRITY.QUESTION q
      on qa.question_id = q.question_id

where q.question = 'Was this SKU a shelf-out when you arrived?' and thd_fiscal_week = '202237' and source in('ZIPPEDI','ZIPPEDI_AISLE_BY_AISLE')
and so.shelf_out_exclusion_reason_id is null
and (so.carry_fwd is not true or shelf_out_session like '%monday%');

![image](https://user-images.githubusercontent.com/17092274/208142192-372be1a2-e862-471c-9fd9-dda044fe1bbc.png)
