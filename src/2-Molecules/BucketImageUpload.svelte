<script lang="ts">
  import FilePond from "../1-Atoms/FilePond.svelte";
  import * as FilePondLib from "filepond";
  import FilePondPluginImageExifOrientation from "filepond-plugin-image-exif-orientation";
  import FilePondPluginImagePreview from "filepond-plugin-image-preview";
  import FilePondPluginFileValidateType from "filepond-plugin-file-validate-type";
  import FilePondPluginImageCrop from "filepond-plugin-image-crop";
  import type { FilePondFile } from "filepond";

  export const registerPlugin = FilePondLib.registerPlugin;
  registerPlugin(
    FilePondPluginImageExifOrientation,
    FilePondPluginImagePreview,
    FilePondPluginFileValidateType,
    FilePondPluginImageCrop
  );

  let pond;

  // pond.getFiles() will return the active files

  // the name to use for the internal file input
  let name = "filepond";
  async function handleAddFile(err, fileItem: FilePondFile) {    
    var result = await window.o.session.saveProfileImage(fileItem.file,fileItem.getMetadata());
    console.log(result);
  }


  window.o.session.getProfileImageMeta().then(resp => console.log(resp));
</script>

<style>
  @import "~filepond-plugin-image-preview/dist/filepond-plugin-image-preview.css";
  @import "~filepond-plugin-image-edit/dist/filepond-plugin-image-edit.css";
</style>

<FilePond
  bind:this={pond}
  {name}
  allowFileTypeValidation={true}
  acceptedFileTypes="image/*"
  allowImageCrop={true}
  imageCropAspectRatio="1:1"
  allowMultiple={false}
  onaddfile={handleAddFile} />
