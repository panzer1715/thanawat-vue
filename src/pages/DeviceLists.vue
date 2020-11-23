<template>
  <div class="container">
    <div class="row my-4">
      <div class="col label text-left">
        <h3>Devices List</h3>
      </div>
      <div class="col text-right">
        <button
          class="btn btn-primary"
          data-toggle="modal"
          data-target="#staticBackdrop"
        >
          Add New Device
        </button>
      </div>
    </div>
    <AddDevice :defaultId="lastDevices"></AddDevice>
    <table class="table table-sm">
      <thead>
        <tr>
          <th>Device ID</th>
          <th>Manufacturer ID</th>
          <th>Device Name</th>
          <th>Device Type</th>
          <th>Price</th>
          <th>Detail</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="device in devices" :key="device.id">
          <th>{{ device.DeviceID }}</th>
          <td>{{ device.ManufacturerID }}</td>
          <td>{{ device.DeviceName }}</td>
          <td>{{ device.DeviceType }}</td>
          <td>{{ device.Price }}</td>
          <th>
            <router-link :to="`/detail/${device.id}`"
              ><i class="fa fa-file-o"></i
            ></router-link>
          </th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import AddDevice from "@/components/AddDevice";
export default {
  name: "DeviceLists",
  components: {
    AddDevice,
  },
  data: () => ({
    devices: [],
    lastDevices: 0,
  }),
  async created() {
    const { data } = await axios.get(
      `https://device-order.herokuapp.com/devices`
    );
    let lastIndex = data.length - 1;
    this.lastDevices = Number(data[lastIndex].DeviceID) + 1;
    this.devices = data.sort((a, b) => b.DeviceID - a.DeviceID);
  },
};
</script>