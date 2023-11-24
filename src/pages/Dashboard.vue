<template>
  <div>
    <!--Stats cards-->
    <div class="row">
      <div
        class="col-md-6 col-xl-3"
        v-for="stats in statsCards"
        :key="stats.title"
      >
        <stats-card>
          <div
            class="icon-big text-center"
            :class="`icon-${stats.type}`"
            slot="header"
          >
            <i :class="stats.icon"></i>
          </div>
          <div class="numbers" slot="content">
            <p>{{ stats.title }}</p>
            {{ stats.value }}
          </div>
          <div class="stats" slot="footer">
            <i :class="stats.footerIcon"></i> {{ stats.footerText }}
          </div>
        </stats-card>
      </div>
    </div>

    <!--Charts-->
    <div class="row">
      <div class="col-12">
        <chart-card
          :title= getBehavior()
          sub-title="24 Hours performance"
          :chart-data="usersChart.data"
          :chart-options="usersChart.options"
        >
          <span slot="footer">
            <i class="ti-reload"></i> Updated 3 minutes ago
          </span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Open
            <i class="fa fa-circle text-danger"></i> Click
            <i class="fa fa-circle text-warning"></i> Click Second Time
          </div>
        </chart-card>
      </div>

      <div class="col-md-6 col-12">
        <chart-card
          :title=getPieChart()
          sub-title="Last campaign performance"
          :chart-data="preferencesChart.data"
          chart-type="Pie"
        >
          <span slot="footer">
            <i class="ti-timer"></i> Campaign set 2 days ago</span
          >
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Open
            <i class="fa fa-circle text-danger"></i> Bounce
            <i class="fa fa-circle text-warning"></i> Unsubscribe
          </div>
        </chart-card>
      </div>

      <div class="col-md-6 col-12">
        <chart-card
          :title=getLineGraph()
          sub-title="All products including Taxes"
          :chart-data="activityChart.data"
          :chart-options="activityChart.options"
        >
          <span slot="footer">
            <i class="ti-check"></i> Data information certified
          </span>
          <div slot="legend">
            <i class="fa fa-circle text-info"></i> Tesla Model S
            <i class="fa fa-circle text-warning"></i> BMW 5 Series
          </div>
        </chart-card>
      </div>
    </div>
  </div>
</template>
<script>
import { StatsCard, ChartCard } from "@/components/index";
import Chartist from "chartist";
export default {
  components: {
    StatsCard,
    ChartCard,
  },
  /**
   * Chart data used to render stats, charts. Should be replaced with server data
   */
  data() {
    return {
      statsCards: null,
      userType: "eng",
      usersChart: {
        data: {
          labels: [
            "9:00AM",
            "12:00AM",
            "3:00PM",
            "6:00PM",
            "9:00PM",
            "12:00PM",
            "3:00AM",
            "6:00AM",
          ],
          series: [
            [287, 385, 490, 562, 594, 626, 698, 895, 952],
            [67, 152, 193, 240, 387, 435, 535, 642, 744],
            [23, 113, 67, 108, 190, 239, 307, 410, 410],
          ],
        },
        options: {
          low: 0,
          high: 1000,
          showArea: true,
          height: "245px",
          axisX: {
            showGrid: false,
          },
          lineSmooth: Chartist.Interpolation.simple({
            divisor: 3,
          }),
          showLine: true,
          showPoint: false,
        },
      },
      activityChart: {
        data: {
          labels: [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "Mai",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
            "Oct",
            "Nov",
            "Dec",
          ],
          series: [
            [542, 543, 520, 680, 653, 753, 326, 434, 568, 610, 756, 895],
            [230, 293, 380, 480, 503, 553, 600, 664, 698, 710, 736, 795],
          ],
        },
        options: {
          seriesBarDistance: 10,
          axisX: {
            showGrid: false,
          },
          height: "245px",
        },
      },
      preferencesChart: {
        data: {
          labels: ["62%", "32%", "6%"],
          series: [62, 32, 6],
        },
        options: {},
      },
    };
  },
  mounted(){
    this.getStats()
  },
  methods:{
    getStats(){
      console.log("called")
      const userType = this.userType;
      if(userType == "marketing"){
      this.statsCards =  [
        {
          type: "warning",
          icon: "ti-server",
          title: "Email Conversion Rate",
          value: "2%",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
        {
          type: "success",
          icon: "ti-wallet",
          title: "Notification Conversion Rate",
          value: "4%",
          footerText: "Last day",
          footerIcon: "ti-calendar",
        },
        {
          type: "danger",
          icon: "ti-pulse",
          title: "Google Ads Conversion Rate",
          value: "2%",
          footerText: "In the last hour",
          footerIcon: "ti-timer",
        },
        {
          type: "info",
          icon: "ti-twitter-alt",
          title: "Twitter Followers Increase",
          value: "+1237",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
      ]
      } else if(userType == "sales"){
        this.statsCards =  [
        {
          type: "warning",
          icon: "ti-server",
          title: "Students Enrolled",
          value: "+123",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
        {
          type: "success",
          icon: "ti-wallet",
          title: "Alumni Fundraising",
          value: "$4350",
          footerText: "Last day",
          footerIcon: "ti-calendar",
        },
        {
          type: "danger",
          icon: "ti-pulse",
          title: "Student Leads Generated",
          value: "+45",
          footerText: "In the last hour",
          footerIcon: "ti-timer",
        },
        {
          type: "info",
          icon: "ti-twitter-alt",
          title: "Applications",
          value: "+230",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
      ]

      } else if(userType == "product"){
        this.statsCards =  [
        {
          type: "warning",
          icon: "ti-server",
          title: "Time Spent on Twitter:",
          value: "150M UAM",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
        {
          type: "success",
          icon: "ti-wallet",
          title: "Monthly Active Users",
          value: "237.2M",
          footerText: "Last day",
          footerIcon: "ti-calendar",
        },
        {
          type: "danger",
          icon: "ti-pulse",
          title: "Social Engagements",
          value: "+137.2M",
          footerText: "In the last hour",
          footerIcon: "ti-timer",
        },
        {
          type: "info",
          icon: "ti-twitter-alt",
          title: "Spam Rate",
          value: "4%",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
      ]

      } else if(userType == "eng"){
        this.statsCards =  [
        {
          type: "warning",
          icon: "ti-server",
          title: "Server RAM Capacity",
          value: "105GB",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
        {
          type: "success",
          icon: "ti-wallet",
          title: "Bugs Reported",
          value: "457",
          footerText: "Last day",
          footerIcon: "ti-calendar",
        },
        {
          type: "danger",
          icon: "ti-pulse",
          title: "Security Errors",
          value: "2",
          footerText: "In the last hour",
          footerIcon: "ti-timer",
        },
        {
          type: "info",
          icon: "ti-twitter-alt",
          title: "System Uptime",
          value: "98.7%",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
      ]

      } else{ // should be e-commerce
      this.statsCards =  [
        {
          type: "warning",
          icon: "ti-server",
          title: "Abandoned Cart Rate",
          value: "40%",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
        {
          type: "success",
          icon: "ti-wallet",
          title: "Repeat Purchase Rate",
          value: "23%",
          footerText: "Last day",
          footerIcon: "ti-calendar",
        },
        {
          type: "danger",
          icon: "ti-pulse",
          title: "Items Refunded Rate",
          value: "30%",
          footerText: "In the last hour",
          footerIcon: "ti-timer",
        },
        {
          type: "info",
          icon: "ti-twitter-alt",
          title: "Avg Review Rating",
          value: "3.9",
          footerText: "Updated now",
          footerIcon: "ti-reload",
        },
      ]

      }

    },
    getBehavior(){
   const userType = this.userType;
      if(userType == "marketing"){
          return "Pizza Orders by Channel (Last 24 Hours)"
     
      } else if(userType == "sales"){
        return "Students Enrollment (By Department)"

      } else if(userType == "product"){
        return "Traffic by User Type (Time Spent)"

      } else if(userType == "eng"){
          return "Engineering Upkeep KPIs"

      } else{ // should be e-commerce
     
      return "Sales by Customer Type"
      }

    },
    getPieChart(){
         const userType = this.userType;
       if(userType == "marketing"){
        return "Pizza Loyalty Program Age Breakdown"

      } else if(userType == "sales"){
        return "Students Enrolled (By Sales Channel)"
      } else if(userType == "product"){
       return "Mobile Time Spent Distribution"

      } else if(userType == "eng"){
        return "Bug Distribution"

      } else{ // should be e-commerce
     
      return "Kith.com Purchases (by Traffic Source)”"
      }

    },
    getLineGraph(){
         const userType = this.userType;
       if(userType == "marketing"){
        return "In-App Notifications A/B Test"
      } else if(userType == "sales"){
       return "Grad vs Undergrad Enrollment"

      } else if(userType == "product"){
       return "Home Timeline A/B Test"

      } else if(userType == "eng"){
          return "Data Accuracy "

      } else{ // should be e-commerce
      return "Top Clothing Products Purchased"

      }

    }
  }
};


</script>
<style></style>
