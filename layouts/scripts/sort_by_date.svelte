<script context="module">
  export const sortByDate = (items, order) => {
    items.sort((a, b) => { 
      // Must have field named "dateCreated" in content source to work.
      let dateA = new Date(a?.fields?.dateCreated.split('/').reverse().join());
      let dateB = new Date(b?.fields?.dateCreated.split('/').reverse().join());
      return (order == "oldest") ? (dateA - dateB) : (dateB - dateA);
    });
    return items;
  };
</script>